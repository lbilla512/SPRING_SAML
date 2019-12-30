Spring Boot Sample SAML 2.0 Service Provider
====================
---------

## References

#### Spring Boot

Spring Boot makes it easy to create Spring-powered, production-grade applications and services with absolute minimum fuss. It takes an opinionated view of the Spring platform so that new and existing users can quickly get to the bits they need.

- **Website:** [http://projects.spring.io/spring-boot/](http://projects.spring.io/spring-boot/)

#### Spring Security SAML Extension

Spring SAML Extension allows seamless inclusion of SAML 2.0 Service Provider capabilities in Spring applications. All products supporting SAML 2.0 in Identity Provider mode (e.g. ADFS 2.0, Shibboleth, OpenAM/OpenSSO, Ping Federate, Okta) can be used to connect with Spring SAML Extension.

- **Website:** [http://projects.spring.io/spring-security-saml/](http://projects.spring.io/spring-security-saml/)

---------

## Project description

This project represents a sample implementation of a **SAML 2.0 Service Provider**, completely built on **Spring Framework**. In particular, it shows how to develop a web solution devised for Federated Authentication, by integrating **Spring Boot** and **Spring Security SAML**. The configuration has been completely defined using *Java annotations* (no XML).

**SSOCircle** ([ssocircle.com](http://www.ssocircle.com/en/portfolio/publicidp/)) is used as public Identity Provider for test purpose.
ssocicle[fengxin58:6Alkrx6<]

## How to running?

1. ssocicle注册账号
2. ngrok http 8080 运行反向代理
3. 运行应用,访问http://xxx.ngrok.io/saml/metadata,获取sp-metadata.xml
4. 将获取到的sp-metadata.xml配置到ssocicle
5. 访问http://xxx.ngrok.io/,一步步操作
6. 在ssocicle做approval的时候,记得要开代理,此处使用的谷歌的防机器人验证码
7. 点击授权即可登陆成功跳转回应用的UI

---------

### Additional notes

1. The certificate on [https://idp.ssocircle.com/](https://idp.ssocircle.com/) seems to change on a fairly regular basis. This results in the following exception. 

`javax.net.ssl.SSLPeerUnverifiedException: SSL peer failed hostname validation for name: null`

To update the SSOCircle certificates within the keystore, just run: 

	cd src/main/resources/saml/ && sh ./update-certifcate.sh 

2. Sometimes SSO Circle could display you an error during the authenticaton process. In this case, please update your federation 
   metadata directly on [https://idp.ssocircle.com](https://idp.ssocircle.com):

	> Manage Metadata > Service Provider Metadata
	
	Remove the current record and add a new one, using your FQDN and providing a new copy of your metadata: your can retrieve them at [http://localhost:8080/saml/metadata](http://localhost:8080/saml/metadata).

3. When the project version corresponds with the Spring Boot parent version, Maven may give you a warning as follows:

	> Version is duplicate of parent version.

	Actually there is nothing wrong with the used configuration, thus you can just ignore that message.