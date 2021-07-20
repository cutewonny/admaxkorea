- 👋 Hi, I’m @admaxkorea
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
admaxkorea/admaxkorea is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

ADMAX Web SDK 적용 가이드
==

1. 연동 절차


a. ADMAX 담당자 혹은 help@ad-max.co.kr로 연락하여 ADMAX Web SDK 광고 집행에 대해서 협의합니다.
b. 협의 완료 후, ADMAX Web SDK 를 삽입할 페이지 URL 을 ADMAX 담당자에게 알려주어 테스트 캠페인을 생성하여 랜딩 URL 을 발급 받습니다.
c. tracker 코드를 사이트의 페이지에 삽입합니다.
d. 페이지 삽입 이후 연동이 되었는지 ADMAX 에서 테스트를 진행합니다.
e. 테스트가 완료되면 광고를 집행합니다.







2. 연동 상세


ADMAX Web SDK 스크립트의 삽입 위치는 아래 2개 페이지에 적용합니다.

랜딩 페이지
전환 완료 페이지
단, 랜딩 페이지와 전환 완료 페이지가 같을 경우 해당 페이지에만 적용하면 되며

해당 페이지 내에서 랜딩 완료 시점과 전환 완료 시점을 구분하여 하기 샘플과 같이 처리하면 됩니다.

더불어, ADMAX Web SDK 스크립트는 head 태그 보다는 body 태그 안쪽의 마지막 부분에 삽입하는 것을 권장합니다.



ADMAX 의 Web SDK 를 삽입하는 광고주 캠페인은 대체로 아래와 같은 흐름이 될 것입니다.

즉, 아래의 흐름 상에 랜딩 페이지와 전환 완료 페이지가 동일한 사이트도 있고, 랜딩 페이지와 전환 완료 페이지가 다른 경우도 있습니다.

또, 랜딩 페이지 이전에 리다이렉트 페이지를 경유하는 사이트도 있고, 랜딩 페이지와 전환 완료 페이지 사이에 경유 페이지가 있는 사이트도 있습니다.



1) 랜딩 페이지와 전환 완료 페이지가 동일한 경우


이 경우 다음 절에서 설명되는 각 캠페인의 랜딩 페이지와 전환 완료 페이지의 샘플 코드가 모두 같은 페이지에 삽입이 되어야 합니다.



2) 랜딩 페이지와 전환 완료 페이지가 다른 경우


이 경우 다음 절에서 설명되는 각 캠페인의 랜딩 페이지와 전환 완료 페이지의 샘플 코드가 각각의 랜딩 페이지 및 전환 완료 페이지에 삽입이 되어야 합니다.

또, 랜딩 페이지와 전환 완료 페이지는 모두 동일한 도메인 내에 위치하고 있어야만 합니다.



3) 랜딩 페이지 전에 리다이렉트 페이지가 있는 경우


이 경우 다음 절에서 설명되는 각 캠페인의 랜딩 페이지와 전환 완료 페이지의 샘플 코드가 각각의 랜딩 페이지 및 전환 완료 페이지에 삽입이 되어야 합니다.

여기에서 가장 중요한 것은 리다이렉트 페이지에서는 ADMAX 클릭 서버를 통해 전달되는 모든 파라메터가 랜딩 페이지까지 전달되도록 해주셔야 합니다.

또, 랜딩 페이지와 전환 완료 페이지는 모두 동일한 도메인 내에 위치하고 있어야만 합니다.



4) 랜딩 페이지와 전환 완료 페이지 사이에 경유 페이지가 있는 경우


이 경우 다음 절에서 설명되는 각 캠페인의 랜딩 페이지와 전환 완료 페이지의 샘플 코드가 각각의 랜딩 페이지 및 전환 완료 페이지에 삽입이 되어야 합니다.

여기에서 가장 중요한 것은 리다이렉트 페이지에서는 ADMAX 클릭 서버를 통해 전달되는 모든 파라메터가 랜딩 페이지까지 전달되도록 해주셔야 합니다.

또, 랜딩 페이지와 전환 완료 페이지는 모두 동일한 도메인 내에 위치하고 있어야만 합니다.









3. 사전예약 캠페인


a. 사전예약 랜딩 페이지

사용자가 사전예약 랜딩 페이지에 도달하면 ADMAX 의 Web SDK 를 초기화 해야 합니다.

아래는 랜딩 페이지에 넣어 주셔야 하는 예제 코드입니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").build();
    tracker.init(initData);
    tracker.firstLanding();
    tracker.open();
</script>
```

b. 사전예약 전환 완료 페이지

사전예약 캠페인의 경우, 전환 완료 시 사용자를 식별할 수 있는 식별자를 넣어주셔야 합니다.
아래 예제 코드와 같이 사용자 개인정보 보호를 위해 SHA1 Hash 된 값으로 처리하는 것을 권장합니다.


더불어, 사용자 식별자를 중복으로 보내서는 안됩니다. 즉, 동일한 사용자가 2번 이상 전환 완료하더라도 최초 1번의 전환만 보내져야 합니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/sha1.js"></script>
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
 
    var strUser = "값" ex) 핸드폰번호, 이메일주소, 주민번호, 즉 유니크한 값 // string으로 적용해주세요
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").setHashId(SHA1(strUser)).build();
    tracker.init(initData);
    tracker.preserveComplete();//전환 포스트백 발송
 
/*
필요할 경우 사용하세요
페이지를 이동해야 하는 경우 '이벤트 리스너 preserve_complete' 사용
    document.addEventListener("preserve_complete", function() {
        ... 광고주 메세지, 집계 혹은 페이지 이동 코드 ...
        alert("완료 메세지");
        location.href = "이동할 페이지";
    });
*/
</script>
```



4. 회원가입 캠페인


a. 회원가입 랜딩 페이지

사용자가 회원가입 랜딩 페이지에 도달하면 ADMAX 의 Web SDK 를 초기화 해야 합니다.

아래는 랜딩 페이지에 넣어 주셔야 하는 예제 코드입니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").build();
    tracker.init(initData);
    tracker.firstLanding();
    tracker.open();
</script>
```

b. 회원가입 전환 완료 페이지

회원가입 캠페인의 경우, 전환 완료 시 사용자를 식별할 수 있는 식별자를 넣어주셔야 합니다.
아래 예제 코드와 같이 사용자 개인정보 보호를 위해 SHA1 Hash 된 값으로 처리하는 것을 권장합니다.


더불어, 사용자 식별자를 중복으로 보내서는 안됩니다. 즉, 동일한 사용자가 2번 이상 전환 완료하더라도 최초 1번의 전환만 보내져야 합니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/sha1.js"></script>
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
 
    var strUser = "값" ex) 핸드폰번호, 이메일주소, 주민번호, 즉 유니크한 값 // string으로 적용해주세요
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").setHashId(SHA1(strUser)).build();
    tracker.init(initData);
    tracker.registration();//전환 포스트백 발송
 
/*
필요할 경우 사용하세요
페이지를 이동해야 하는 경우 '이벤트 리스너 registration_complete' 사용
    document.addEventListener("registration_complete", function() {
        ... 광고주 메세지, 집계 혹은 페이지 이동 코드 ...
        alert("완료 메세지");
        location.href = "이동할 페이지";
    });
*/
 
</script>
```



5. 상품구매 캠페인


a. 상품구매 랜딩 페이지

사용자가 상품구매 랜딩 페이지에 도달하면 ADMAX 의 Web SDK 를 초기화 해야 합니다.

아래는 랜딩 페이지에 넣어 주셔야 하는 예제 코드입니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").build();
    tracker.init(initData);
    tracker.firstLanding();
    tracker.open();
</script>
```

b. 상품구매 전환 완료 페이지

상품구매 캠페인의 경우, 전환 완료 시 사용자를 식별할 수 있는 식별자와 함께 사용자가 구매한 항목들과 주문 정보를 넣어주셔야 합니다.
아래 예제 코드와 같이 사용자 개인정보 보호를 위해 SHA1 Hash 된 값으로 처리하는 것을 권장합니다.


```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/sha1.js"></script>
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
     
 
    var strUser = "값" ex) 핸드폰번호, 이메일주소, 주민번호, 즉 유니크한 값 // string으로 적용해주세요
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").setHashId(SHA1(strUser)).build();
    tracker.init(initData);
  
    /* STAR LOOP: 구매한 모든 상품에 대해 */
    tracker.PurchaseEvent.addPurchase("상품ID", "상품단가", "상품구매갯수"); // 상품단가에서 ,(콤마)를 제거한 숫자만 전달해주세요 ex)"165,000"(x) -> "165000"(o)
    /* END LOOP */
  
    tracker.PurchaseEvent.setOrder("주문ID", "총 주문 가격");
  
    var purchaseEvent = tracker.PurchaseEvent.build();
    tracker.purchase(purchaseEvent);//전환 포스트백 발송
 
/*
필요할 경우 사용하세요
페이지를 이동해야 하는 경우 '이벤트 리스너 purchase_complete' 사용
    document.addEventListener("purchase_complete", function() {
        ... 광고주 메세지, 집계 혹은 페이지 이동 코드 ...
        alert("완료 메세지");
        location.href = "이동할 페이지";
    });
*/
</script>
```



6. CPC 캠페인


a. CPC 랜딩 페이지

CPC 캠페인의 경우 ADMAX 와 광고주 간 협의에 따라 사용자가 랜딩 페이지에 도달하여 몇 초를 머물렀는지에 따라 전환 처리가 되므로 전환 완료 페이지는 필요가 없습니다.

이에 따라 사용자가 CPC 랜딩 페이지에 도달하면 ADMAX 의 Web SDK 를 초기화 하고 또 전환 완료 처리 코드도 함께 넣어주면 정해진 시간이 지났을 때 전환 처리가 됩니다.

아래는 랜딩 페이지에 초기화 코드와 더불어 전환 처리 코드를 넣어 주시는 예제 코드입니다.


```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").build();
    tracker.init(initData);
    tracker.firstLanding();
    tracker.open();
    tracker.triggerCpc();
</script>
```

위의 예제 코드는 사용자가 CPC 랜딩 페이지에 일정 시간을 머물렀을 때 ADMAX 로 Postback 을 보내고 끝나게 됩니다만

광고주 측에서도 이렇게 Postback 을 발송한 사항을 집계하기를 원할 수 있습니다.

이 경우에는 아래 예제 코드와 같이 Postback 을 발송한 시점에 event 를 받아 확인할 수 있습니다.

```javascript
<script type="text/javascript" src="//s3.ap-northeast-2.amazonaws.com/vegas-kor-o/sdk/web/vegastracker.min.js"></script>
<script type="text/javascript">
 
 
    var tracker = new VegasTracker();
    var initData = tracker.InfoBuilder.setCountry("KR").build();
    tracker.init(initData);
    tracker.firstLanding();
    tracker.open();
    tracker.triggerCpc();//전환 포스트백 발송.
 
 
/*
필요할 경우 사용하세요
페이지를 이동해야 하는 경우 '이벤트 리스너 cpc_complete' 사용
    document.addEventListener("cpc_complete", function() {
        ... 광고주 메세지, 집계 혹은 페이지 이동 코드 ...
        alert("완료 메세지");
        location.href = "이동할 페이지";
    });
*/
</script>
```

