# 01. 암호학 개요
(1) 암호화와 복호화
---

|암호화와 복호화|
|-|
|![이미지](./img/01.png)|

<br>

> 💡
```
  * 용어
    - 암호화 : Encrypt
    - 복호화 : Decrypt
    - 평문 : Plaintext
    - 암호문 : Ciphertext
    - 키 : Key

  * C = Ek(P) : 평문 P를 키 k로 암호화하여(E) 암호문 C를 얻음

  * P = Dk(C) : 암호문 C를 키 k로 복호화하여(D) 평문 P를 얻음
```

<br>

---

<br>

(2) 암호화 시스템

<table>
  <tr>
    <th colspan=4>구분</th>
    <th>종류</th>
    <th>비고</th>
  </tr>
  <tr>
    <td rowspan=6>양<br>방<br>향</td>
    <td rowspan=4>대칭키</td>
    <td rowspan=2>Stream<br>방식</td>
    <td>동기식</td>
    <td>OTP, FSR, LFSR, NLFSR, OFB, RC4</td>
    <td>난수열(키스트림) 독립적 생성</td>
  </tr>
  <tr>
    <td>비동기식<br>(자기동기식)</td>
    <td>CFB</td>
    <td>난수열 종속적 생성</td>
  </tr>
  <tr>
    <td rowspan=2>Block<br>방식</td>
    <td>Feistel</td>
    <td>DES, SEED</td>
    <td>암호화 과정 = 복호화 과정</td>
  </tr>
  <tr>
    <td>SPN</td>
    <td>Fijndael, ARIA</td>
    <td>암호화 과정 != 복호화 과정</td>
  </tr>
  <tr>
    <td rowspan=2>비대칭키</td>
    <td colspan=2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;소인수분해 문제</td>
    <td>RSA</td>
    <td>기밀성, 인증, 부인방지</td>
  </tr>
  <tr>
    <td colspan=2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;이산대수 문제</td>
    <td>ECC, ElGamal, DH</td>
    <td>기밀성, 인증, 부인방지</td>    
  </tr>
  <tr>
    <td rowspan=3>일<br>방<br>향</td>
    <td rowspan=3>해시함수</td>
    <td>MDC</td>
    <td>해시함수</td>
    <td>MD5, SHA-1, RIPEMD, HAS-160</td>
    <td>무결성</td>    
  </tr>
  <tr>
    <td>MAC</td>
    <td>해시함수 + 대칭키</td>
    <td>축소 MAC, HMAC, CBC-MAC</td>
    <td>무결성 + 인증</td>      
  </tr>
  <tr>
    <td>전자서명</td>
    <td>해시함수 + 비대칭키</td>
    <td>RSA 전자서명, DSS, ECDSA, KCDSA</td>
    <td>무결성 + 인증 + 부인방지</td>         
  </tr>
</table>

<br>

---

<br>

(3) 암호기법의 분류
---
- **치환 암호와 전치 암호**

  - 치환 암호(대치 암호)
 
    - 비트, 문자 또는 문자의 블록을 다른 비트, 문자 또는 블록으로 대체, 교환하는 규칙
   
  - 전치암호
 
    - 비트, 문자 또는 블록이 원래 의미를 감추도록 재배열, 자리를 바꾸는 규칙

- **블록 암호와 스트림 암호**

  - 블록 암호
 
    - 특정 비트 수의 `집합`을 한 번에 처리하는 암호 알고리즘의 총칭
   
  - 스트림 암호
 
    - 한번에 1비트 혹은 1바이트의 데이터 흐름(스트림)을 순차적으로 처리해가는 암호 알고리즘의 총칭
   
- **위치에 따른 암호화 구분**

  - 링크 암호화
 
    - 모든 정보는 암호화되고, 패킷은 라우터나 다른 중간에 있는 장비가 이 패킷을 다음 어디로 보내야 하는지 알아야 하기 때문에 각 홉(hop)에서 해독됨
   
  - 종단간 암호화
 
    - 종단간 암호화에서는 헤더와 트레일러가 암호화되지 않기 때문에 패킷을 각 홉에서 해독하고 암호화할 필요 없음

- **HW 암호와 SW 암호**

  - 하드웨어 암호
 
    - 하드웨어로 실현하기 위해 컴퓨터와 통신기기의 내부버스와 외부 인터페이스에 전용 암호처리용 하드웨어를 설치하여 데이터를 암호화
   
  - 소프트웨어 암호
 
    - 소프트웨어로 실현하기 위해 암호처리용 소프트웨어를 사용하여 데이터를 암호화

<br>

---

<br>

(4) 암호분석의 분류
---

|구분|영어|개념|비고|
|:-:|:-:|-|-|
|암호문<br>단독 공격|COA<br>Ciphertext Only Attack|- 단지 암호문 C만을 갖고 이로부터<br>&nbsp;&nbsp;&nbsp;&nbsp;평문 P나 키 k를 찾아내는 방법<br>- 평문 P의 통계적 성질, 문장의 특성 등을<br>&nbsp;&nbsp;&nbsp;&nbsp;추정하여 해독하는 방법|암호해독자에게는 가장<br>불리한 방법|
|기지<br>평문 공격|KPA<br>Known Plaintext Attack|암호문 C와 평문 P의 관계로부터 키 k나<br>평문 P를 추정하여 해독하는 방법|암호문에 대응하는 일부 평문이<br>사용가능한 상황에서의 공격|
|선택<br>평문 공격|CPA<br>Chosen Plaintext Attack|암호기에 접근할 수 있어 평문 P를 선택하여<br>그 평문 P에 해당하는 암호문 C를 얻어 키 k나<br>평문 P를 추정하여 암호를 해독하는 방법|평문을 선택하면 대응하는<br>암호문을 얻을 수 있는<br>상황에서의 공격|
|선택<br>암호문 공격|CCA<br>Chosen Ciphertext Attack|암호 복호기에 접근할 수 있어 암호문 C에<br>대한 평문 P를 얻어내 암호를 해독하는 방법|암호문을 선택하면 대응하는<br>평문을 얻을 수 있는<br>상황에서의 공격|

<br>

> 💡
```
  * 암호해독(암호분석)
    - 암호방식의 정규 참여자가 아닌 제3자가 암호문으로부터 평문을 찾으려는 시도

  * 암호해독자는 평문과 키를 찾아내는 것을 목표로 함

  * 케르히호프의 원리(Kerckhoff's principle)
    - 암호학에서 암호해독자는 현재 사용되고 있는 암호방식을 알고 있다는 전제하에 암호해독을 시도하는 것으로 간주
```

<br>

---

<br>











