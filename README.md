# Customized aggregation subscription CF-Workers-SUB

### This is a link built through Cloudflare Workers, which aggregates any of your nodes and multiple subscriptions into a subscription link that is exclusive to you

Telegram communication group: [@CMLiussss](https://t.me/CMLiussss), **Thanks to [Alice Networks](https://alicenetworks.net/) for providing cloud servers to maintain [CM subscription conversion service](https://sub.fxxk.dedyn.io/)! **

## Pages deployment method [video tutorial](https://youtu.be/9npcBXZTSe4)
### 1. Deploy Cloudflare Pages:
- Fork this project on Github and click Star!!!
- After selecting `Connect to Git` in the Cloudflare Pages console, select the `CF-Workers-SUB` project and click `Start Setting`.

### 2. Bind a custom domain to Pages:
- In the `Custom Domains` tab of the Pages console, click `Set Custom Domain` at the bottom.
- Fill in your custom subdomain name, and be careful not to use your root domain name, for example:
If the domain name you are assigned is `fuck.cloudns.biz`, then add a custom domain and fill in `sub.fuck.cloudns.biz`;
- According to Cloudflare's requirements, your domain name DNS service provider will be returned. After adding the CNAME record `CF-Workers-SUB.pages.dev` of the custom domain `sub`, click `Activate Domain`.

### 3. Modify the quick subscription entry:

For example, your pages project domain name is: `sub.fuck.cloudns.biz`;
- Add the `TOKEN` variable, quick subscription access entry, the default value is: `auto`, get the subscriber's default node subscription address, which is `/auto`, for example `https://sub.fuck.cloudns.biz/auto`

### 4. Add your node and subscription link:
- Add the `LINK` variable, add your self-built node link and airport subscription link as parameters, and make sure there is one link per line, for example:
```
vless://b7a392e2-4ef0-4496-90bc-1c37bb234904@cf.090227.xyz:443?encryption=none&security=tls&sni=edgetunnel-2z2.pages. dev&fp=random&type=ws&host=edgetunnel-2z2.pages.dev&path=%2F%3Fed%3D2048#%E5%8A%A0%E5%85%A5%E6%88%91%E7%9A%84%E9%A2%9 1%E9%81%93t.me%2FCMLiussss%E8%A7%A3%E9%94%81%E6%9B%B4%E5%A4%9A%E4%BC%98%E9%80%89%E8%8A%82%E7%82%B9 vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIuWKoOWFpeaIkeeahOmikemBk3QubWUvQ01MaXVzc3Nz6Kej6ZSB5pu05aSa5LyY6YCJ6IqC54K5PuiLseWbvSDlgKvmlabp h5Hono3ln44iLA0KICAiYWRkIjogImNmLjA5MDIyNy54eXoiLA0KICAicG9ydCI6ICI4NDQzIiwNCiAgImlkIjogIjAzZmNjNjE4LWI5M2QtNjc5Ni02Y WVkLThhMzhjOTc1ZDU4MSIsDQogICJhaWQiOiAiMCIsDQogICJzY3kiOiAiYXV0byIsDQogICJuZXQiOiAid3MiLA0KICAidHlwZSI6ICJub25lIiwNCi AgImhvc3QiOiAicHBmdjJ0bDl2ZW9qZC1tYWlsbGF6eS5wYWdlcy5kZXYiLA0KICAicGF0aCI6ICIvamFkZXIuZnVuOjQ0My9saW5rdndzIiwNCiAgInR scyI6ICJ0bHMiLA0KICAic25pIjogInBwZnYydGw5dmVvamQtbWFpbGxhenkucGFnZXMuZGV2IiwNCiAgImFscG4iOiAiIiwNCiAgImZwIjogIiINCn0=
https://sub.xf.free.hr/auto
https://hy2sub.pages.dev
```

## Workers deployment method
### 1. Deploy Cloudflare Worker:

- Create a new Worker in the Cloudflare Worker console.
- Paste the content of [worker.js](https://github.com/cmliu/CF-Workers-SUB/blob/main/_worker.js) into the Worker editor.

### 2. Modify the subscription entry:

For example, the domain name of your workers project is: `sub.cmliussss.workers.dev`;
- Modify the value of `mytoken` to modify the entry of your exclusive subscription to avoid subscription leakage.
```
let mytoken = 'auto';
```
As shown above, your subscription address is as follows:
```url
https://sub.cmliussss.workers.dev/auto
or
https://sub.cmliussss.workers.dev/?token=auto
```

### 3. Add your node or subscription link:

**3.1 Example of modifying the MainData parameter**

- Modify the `MainData` parameter to add your self-built node, for example:

```js
const MainData = `
vless://b7a392e2-4ef0-4496-90bc-1c37bb234904@cf.090227.xyz:443?encryption=none&security=tls&sni=edgetunnel-2z2.pages.dev&fp=random&type=ws&host=edgetunnel-2z2.pages.d ev&path=%2F%3Fed%3D2048#%E5%8A%A0%E5%85%A5%E6%88%91%E7%9A%84%E9%A2%91%E9%81%93t.me% 2FCMLiussss%E8%A7%A3%E9%94%81%E6%9B%B4%E5%A4%9A%E4%BC%98%E9%80%89%E8%8A%82%E7%82%B9
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIuWKoOWFpeaIkeeahOmikemBk3QubWUvQ01MaXVzc3Nz6Kej6ZSB5pu05aSa5LyY6YCJ6IqC54K5PuiLseWbvSDlgKvmlabph5Hono3ln44iLA0 KICAiYWRkIjogImNmLjA5MDIyNy54eXoiLA0KICAicG9ydCI6ICI4NDQzIiwNCiAgImlkIjogIj AzZmNjNjE4LWI5M2QtNjc5Ni02YWVkLThhMzhjOTc1ZDU4MSIsDQogICJhaWQiOiAiMCIsDQogIC JzY3kiOiAiYXV0byIsDQogICJuZXQiOiAid3MiLA0KICAidHlwZSI6ICJub25lIiwNCiAgImhvc 3QiOiAicHBmdjJ0bDl2ZW9qZC1tYWlsbGF6eS5wYWdlcy5kZXYiLA0KICAicGF0aCI6ICIvamFkZ XIuZnVuOjQ0My9saW5rdndzIiwNCiAgInRscyI6ICJ0bHMiLA0KICAic25pIjogInBwZnYydGw5dmVvamQtbWFpbGxhenkucGFnZXMuZGV2IiwNCiAgImFscG4iOiAiIiwNCiAgImZwIjogIiINCn0=
`
```
Note! The special quotes of the `MainData` parameter must be retained, otherwise the code will be abnormal.

**3.2 Example of modifying the urls parameter**

- Modify the `urls` parameter and set the `urls` variable in the script to the URL of your subscription link. For example:

```js
const urls = [
'https://sub.xf.free.hr/auto',
'https://hy2sub.pages.dev',
];
```
Note! The subscription link content must be in `base64` format.

## Variable description
| Variable name | Example | Remarks |
|--------|---------|-----|
| LINK | vless://b7a39... vmess://ew0K... https://sub... | Multiple node links and multiple subscription links can be placed at the same time, and the links are separated by line breaks |
| TOKEN | auto | Subscription path address for quick subscription of built-in nodes /auto |
| TGTOKEN | 6894123456:XXXXXXXXXX0qExVsBPUhHDAbXXXXXqWXgBA | Robot token for sending TG notifications |
| TGID | 6946912345 | Account digital ID for receiving TG notifications |
| SUBAPI | subapi.fxxk.dedyn.io | Subscription conversion backend such as clash and singbox |
| SUBCONFIG | [https://raw.github.../ACL4SSR_Online_MultiCountry.ini](https://raw.githubusercontent.com/cmliu/ACL4SSR/main/Clash/config/ACL4SSR_Online_MultiCountry.ini) | clash, singbox, etc. Subscription conversion configuration file |

## Notes
In the project, TGTOKEN and TGID need to be registered and obtained on Telegram before use. Among them, TGTOKEN is the credential of the telegram bot, and TGID is the ID of the telegram user or group used to receive notifications.

## Star Stars rise [![Stargazers over time](https://starchart.cc/cmliu/CF-Workers-SUB.svg?variant=adaptive)](https://starchart.cc/cmliu/CF-Workers-SUB) # Acknowledgments <a href="https://alicenetworks.net/"><img src="https://alicenetworks.net/templates/lagom2/assets/img/logo/logo_big.194980063.png" width="150" height="75" alt="Alice Networks LTD"/></a>, [mianayang](https://github.com/mianayang/myself/blob/main/cf-workers/sub/sub.js), [ACL4SSR](https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash/config), [fat sheep](https://github.com/youshandefeiyang/sub-web-modify)