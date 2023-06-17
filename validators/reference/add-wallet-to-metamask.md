# Add your validator wallet to metamask

To add your validator EVM wallet address to metamask follow these steps:

&#x20;

**Step 1: Export your private key for metamask**


<pre class="language-javascript"><code class="lang-javascript"><strong>cascadiad keys export &#x3C;key_name> --unarmored-hex --unsafe
</strong></code></pre>

Replace `<key_name>` with your validator's key name.

\
**For example:**

```
cascadiad keys export yourvalidator --unarmored-hex --unsafe
```
After submitting the command a warning is displayed:
```
WARNING: The private key will be exported as an unarmored hexadecimal string. USE AT YOUR OWN RISK. Continue? [y/N]:
```
answer **y** and input your **keyring passphrase** when requested.

Finally, copy the private key. It is a 64 char alphanumeric string. 

&#x20;

**Step 2: import the account on Metamask using the private key you exported in step 1**


Open the Metamask extension from your browser and switch to **Cascadia testnet**

![image](https://github.com/barolosan/docs/assets/118662233/86097dbe-4fc3-4f4c-835c-909b1e5f5bcb)

Click the circle icon at the top right corner of your MetaMask pop-up next to the network indicator and select **Import Account** on the dropdown menu

![image](https://github.com/barolosan/docs/assets/118662233/93a50f95-f99a-4f17-831c-68b665a2f858)

Paste your private key in the text box and click **import**

![image](https://github.com/barolosan/docs/assets/118662233/4bbd8c6a-734a-45ca-8c14-34d0972871af)

**Well Done! You imported your validator wallet on Metamask!**

![image](https://github.com/barolosan/docs/assets/118662233/3a2c595e-c58f-4a46-96b9-23f871ae1c92)


