https://zhuanlan.zhihu.com/p/53329356


Server

创建密钥数据库并设置数字证书。

-----------------------------------------------------------------------------------------------------------------------------
## Key database files

### .kdb

A key database stores key pairs and digital certificates, and enables secure network connections between clients and servers.
In FIPS 140-2 mode, passwords for key databases must meet the following requirements. If passwords do not meet these requirements, the key database is created, but you are unable to create, sign, or receive certificates and an error is written to the ObjectServer log.

    The minimum password length is 14 characters.
    A password must have at least one lower case character, one upper case character, and one digit or special character.
    Each character must not occur more than three times in a password.
    No more than two consecutive characters of the password can be identical.
    All characters are in the standard ASCII printable character set within the range from 0x20 to 0x7E inclusive.
    
### .rdb

When a certificate request is created, a .rdb file is created to store the requested key pair and the certificate request data. When a signed certificate is obtained from a CA and received into the key database, the signed certificate is matched up with the private key in the .rdb file and together they are added to the .kdb file as a certificate and its private key information. The request entry is then deleted from the request key database. 


### .crl

A .crl file is created for legacy reasons and is no longer used. This file was used to store a certificate revocation list (CRL) detailing revoked or suspended certificates. 


### .sth

You can save the password for a key database to a stash file if you require automatic login to the key database in order to gain access to the digital certificates. The password is stored in encrypted format in the stash file.

Whenever the key database is accessed, the system checks whether a stash file exists. If found, the file contents are decrypted and used as input for the password. 

------------------------------------------------------------------------------------------------------------------------------
