在之前的代码中，实现文件加密和解密的主要步骤如下：

### 文件选择与密码输入

用户可以通过文件输入框选择要加密或解密的文件，并在密码输入框中输入密码。

### 生成随机密码

用户可以点击“生成密码”按钮，代码会生成一个随机密码并填入密码输入框。生成随机密码的过程如下：

```javascript
function generateKey() {
    const usedChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789@#_+=";
    let keyArray = new Uint8Array(16);
    window.crypto.getRandomValues(keyArray);
    keyArray = keyArray.map(x => usedChars.charCodeAt(x % usedChars.length));
    const randomizedKey = String.fromCharCode.apply(null, keyArray);
    password.value = randomizedKey;
    keyCheckMeter();
}
```

- 这里使用 `crypto.getRandomValues` 生成一个16字节的随机数，然后将其映射到指定字符集，最终生成一个随机密码。

### 加密文件

加密文件的过程主要在 `encryptFile` 函数中实现，步骤如下：

1. **导入密钥**：将用户输入的密码转换为密钥。
   
   ```javascript
   async function importSecretKey() {
    let rawPassword = str2ab(password.value);
    return window.crypto.subtle.importKey("raw", rawPassword, {
        length: DEC.algoLength,
        name: DEC.algoName1
    }, false, DEC.perms1);
   }
   ```
2. **派生加密密钥**：使用导入的密钥和其他参数（如盐值和迭代次数）派生出加密密钥。
   
   ```javascript
   async function deriveEncryptionSecretKey() {
    let getSecretKey = await importSecretKey();
    let rawPassword = str2ab(password.value);
    return window.crypto.subtle.deriveKey({
        name: DEC.algoName1,
        salt: DEC.salt,
        iterations: DEC.itr,
        hash: {
            name: DEC.hash
        }
    }, getSecretKey, {
        name: DEC.algoName2,
        length: DEC.algoLength
    }, false, DEC.perms2);
   }
   ```
3. **读取文件内容**：使用 `FileReader` 读取用户选择的文件。
4. **加密文件内容**：使用派生的密钥和初始化向量（IV）对文件内容进行加密。
   
   ```javascript
   const iv = window.crypto.getRandomValues(new Uint8Array(16));
   const content = new Uint8Array(fr.result);
   await window.crypto.subtle.encrypt({
    iv: iv,
    name: DEC.algoName2
   }, derivedKey, content).then(function(encrypted) {
    resolve(processFinished("Encrypted-" + file.name, [window.atob(DEC.signature), iv, DEC.salt, new Uint8Array(encrypted)], 1, password.value));
    resetInputs();
   }).catch(function(err) {
    errorMsg("在加密文件时发生了错误，请重新操作!");
   });
   ```
- 这里使用 `crypto.subtle.encrypt` 方法进行加密，传入的参数包括加密算法、密钥、文件内容和IV。

### 解密文件

解密文件的过程主要在 `decryptFile` 函数中实现，步骤如下：

1. **导入密钥**：与加密过程相同，将用户输入的密码转换为密钥。
2. **派生解密密钥**：使用导入的密钥和其他参数派生出解密密钥。
3. **读取加密文件内容**：使用 `FileReader` 读取用户选择的加密文件。
4. **解密文件内容**：使用派生的密钥和IV对文件内容进行解密。
   
   ```javascript
   await window.crypto.subtle.decrypt({
    iv: iv,
    name: DEC.algoName2
   }, derivedKey, content).then(function(decrypted) {
    resolve(processFinished(file.name.replace("Encrypted-", ""), [new Uint8Array(decrypted)], 2, password.value));
    resetInputs();
   }).catch(function() {
    errorMsg("您输入了一个错误的解密密码!");
   });
   ```
- 这里使用 `crypto.subtle.decrypt` 方法进行解密，传入的参数与加密时相同。

### 结果处理

- 加密和解密完成后，代码会处理结果，生成下载链接并显示在页面上。

### 总结

整个加密和解密流程涉及到用户输入的密码处理、文件内容的读取、密钥的导入和派生、以及进行实际的加密和解密操作。代码结构清晰，功能模块化，确保了安全性和用户友好性。


