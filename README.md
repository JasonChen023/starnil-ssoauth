# STARNIL-SSOAUTH�����¼�����


## һ����Ŀ����
��Ŀ����Servletʵ�ֵ�һ��SSO��֤������������server��client�ˡ���Ŀ���������ݿⲿ�����ݣ�
server�˶����û���¼��ֻ֤�ṩһ����֤������ʾ�����轫�����Ӧ�õ�����ϵͳ��������ʵ��ϵͳ��ָ���ӿڽ�����չ���ɡ�


### 1.1����������

��������ʵ���û���֤���˳���¼����ϵͳͬ���˳�����������⣨�����Token��֤�������û������Լ���¼�û�Ticket���ݻ��档


### 1.2����������

�ͻ���ͨ��Filter����ָ����Դ/ҳ�棬�Ա��������ݽ�����֤��������ز����ڵ�¼�û���Ϣ��session�����ض��򵽷������˽�����֤��
��֤ͨ���󷵻�������Դ/ҳ�棨һ������Token����

### 1.3���˺���Ϣ

ϵͳĬ���˺ż����룺admin��



## ������֤����
![image](https://github.com/starnil/starnil-ssoauth/blob/master/doc/%E8%AE%A4%E8%AF%81%E6%B5%81%E7%A8%8B.png)

## ����������չ
���֧�ֶԵ�¼ҵ���߼�����¼�û��������ݽ�����չ��������е�¼��֤Ĭ�ϲ���SSOLogin�ࣨʵ��Login�ӿڣ������ݻ�����ñ��ػ��漰SSOCacheImpl�ࣨʵ��SSOCache�ӿڣ���

### 3.1����¼��֤��չ��ʵ��Login�ӿڣ�
**�ο�SSOLogin��**
����Ҫ������ݿ⼰ҵ��ϵͳʹ�ø���������ڵ�¼ֻ��Ҫ����һ��ʵ���ಢʵ��Login�ӿڣ�ͬʱ��Ҫ�Ѹ�����web.xml������ָ����������֤��Servlet���ɡ�
```java
public class SSOLogin implements Login {

 @Override
 public LoginStatus verify(String userName, String password, String imgCode) {
  LoginStatus ls = new LoginStatus();
  if("admin".equals(userName) && "admin".equals(password)) {
   String userId = GUIDUtil.uuid();
   SSOUser user = new SSOUser(); // ����һ�� user����
   user.setId(userId); // userId��ȷ��Ψһ������SSO�ڴ����û���������ʱ��Ϊid��ͬ�ᵼ�����ݳ�ͻ�����𲻿�Ԥ���Դ���
   user.setName(userName); // ���룬�û��������ظ��ͻ��ˡ�
   ls.setState(1000); // ��¼�ɹ�����1000�����룩
   // ��¼�ɹ��������LoginStatus����һ����ȷ��SSOUser���󣨰����û�ID���û����������ڴ���SSOϵͳ���û���Ϣ�á�
   ls.setUser(user);
  } else {
   ls.setState(444);
  }
  return ls;
 }
}
```

## �ġ�demo����