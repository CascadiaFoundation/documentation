# Upgrade

Follow these steps to upgrade your Cascadia node.\


**Step 1: Stop the `cascadiad` service.**

```javascript
sudo systemctl stop cascadiad
```

\
**Step 2: Navigate to the home directory.**

```javascript
cd $HOME
```

\
**Step 3: Download the latest Cascadia release.**

{% code overflow="wrap" %}
```javascript
curl -L https://github.com/CascadiaFoundation/cascadia/releases/download/v0.1.3/cascadiad-v0.1.3-linux-amd64 -o cascadiad
```
{% endcode %}

{% hint style="info" %}
The latest `cascadiad` binary release can be found on [GitHub](https://github.com/cascadiafoundation/cascadia/releases).
{% endhint %}

\
**Step 4: Make the downloaded file executable.**

```javascript
chmod +x cascadiad
```

\
**Step 5: Replace the existing Cascadia binary with the latest version.**

```javascript
sudo mv cascadiad $(which cascadiad)
```

\
**Step 6: Restart the `cascadiad` service.**

```javascript
sudo systemctl restart cascadiad
```
