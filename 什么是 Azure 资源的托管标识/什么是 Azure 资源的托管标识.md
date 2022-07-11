# 什么是 Azure 资源的托管标识？

开发人员面临着一个共同的挑战，那就是如何管理用于保护服务之间通信安全的机密、凭据、证书和密钥。

**托管标识使开发人员无需管理这些凭据. **

虽然开发人员可以安全地将机密存储在 Azure Key Vault 中，
但服务需要一种方法来访问 Azure Key Vault。 
托管标识在 Azure Active Directory 中提供了自动托管标识，
供应用程序在连接到支持 Azure Active Directory (Azure AD) 身份验证的资源时使用。 
应用程序可以使用托管标识来获取 Azure AD 令牌，而无需管理任何凭据。
