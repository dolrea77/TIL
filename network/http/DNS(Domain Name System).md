# DNS(Domain Name System)



## DNS란

외우기 어려운 ip주소를 외우기 쉽도록 이름을 붙인 시스템을 뜻함 



## 동작과정

1. 도메인 주소를 주소창을 통하여 검색
2. 브라우저에서 DNS Resolver에 연락을 한다
3. DNS Resolver에서 Root Server로가서 .com, .net  같은 TLD를 구분하여 담당 TLD Server로 보내라고 응답ex) .com 담당 TLD Server 
4. DNS Resolver는 응답을 받아 담당TLD Server로 요청을 보낸다 
5. TLD Server는 해당 도메인 Name Server에 보내라고 응답
6. DNS Resolver는 해당 도메인 Name Server에 요청 
7. 레코드에서 원하는 주소(A레코드에는 ipv4주소있다)를 DNS Resolver에게 응답 
8. 브라우저는 DNS Resolver에게서 ip주소 응답을 받음
9. 브라우저는 해당 ip로 server에 해당 페이지를 요청 
10. server에서 해당 페이지를 응답 

- 위 과정은 복잡하기 때문에 캐시를 사용하여 ip주소를 저장 해두고 사용시 마다 바로 ip주소를 사용할 수 있도록 하여 최적화를 할 수 있다  
- 레코드 종류
  - A : IPv4
  - AAAA : IPv6
  - CNAME : Canonical Name record
    - aaa.com 이라는 도메인을 사용한다면 aaa.com으로만 접속이 되고 www.aaa.com은 연결이 되지 않는다 하지만 CNAME으로 www.aaa.com과 aaa.com을 연결을 해둔다면 www.aaa.com으로도 접속을 할 수 있게된다 