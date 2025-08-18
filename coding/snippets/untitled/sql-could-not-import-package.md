# SQL - Could not import package

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Run this before importing

```
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'contained database authentication', 1;
RECONFIGURE;
GO
```
