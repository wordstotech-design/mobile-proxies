# Mobile Proxies

A practical reference for **mobile proxies**: what a 4G mobile proxy is, how 3G, 4G, and 5G differ, when to pick rotating over static, and how to connect in Python, Node.js, and cURL. Mobile proxies route through real mobile carrier IPs, which gives them the highest trust of any proxy type for mobile-first platforms and apps.

The target keywords for this repo are mobile proxies, 4g mobile proxy, 4g proxy, and rotating mobile proxies. [Proxy-Cheap](https://www.proxy-cheap.com/) is the reference service, with per-GB pay-as-you-go billing on its rotating mobile line.

## What a 4G mobile proxy is

A 4G mobile proxy routes your request through an IP that a mobile carrier assigned to a real device on its 4G network. To the destination, the traffic carries a mobile carrier identity rather than a datacenter or fixed-line one. Carriers hand the same pool of IPs to thousands of real subscribers, which is what gives mobile IPs their trust profile.

The network generation sets the speed ceiling:

| Network | Speed | Notes |
|---|---|---|
| 5G | Fastest | Newest generation, best for throughput |
| 4G / LTE | Fast | The common choice, wide availability |
| 3G | Slowest | Legacy, still useful where 4G is absent |

A 4G proxy is the practical default: fast enough for most workloads and broadly available across carriers and countries.

## Why mobile proxies

Mobile carrier IPs suit workloads that target mobile-first platforms or need a carrier-grade identity:

- **Social media multi-account management**, where each account benefits from a mobile IP.
- **Mobile app quality assurance**, testing how an app behaves from a carrier network.
- **Ad verification** on mobile placements.
- **Market and price research** across mobile storefronts.

## Rotating vs static mobile

- **Rotating mobile.** The IP changes automatically per session from a large carrier pool. Use it for distributed workloads where varied IPs help. Billed per GB, pay-as-you-go.
- **Static mobile.** A fixed mobile IP held for the subscription, with the option to rotate it on demand from the dashboard. Use it for account-bound tasks that want a stable carrier identity.

Pick rotating for volume and variety, static for a steady identity you control.

## Connecting

A mobile proxy is addressed as `HOST:PORT` with credentials from your provider dashboard. The format is identical across clients.

cURL:

```bash
curl -x http://USERNAME:PASSWORD@MOBILE_PROXY_HOST:PORT https://api.ipify.org
```

Python (`requests`):

```python
import requests

proxy = "http://USERNAME:PASSWORD@MOBILE_PROXY_HOST:PORT"

response = requests.get(
    "https://api.ipify.org",
    proxies={"http": proxy, "https": proxy},
    timeout=30,
)
print("Exit IP:", response.text)
```

Node.js (`axios`):

```javascript
const axios = require('axios');

axios.get('https://api.ipify.org', {
    proxy: {
        protocol: 'http',
        host: 'MOBILE_PROXY_HOST',
        port: PORT,
        auth: { username: 'USERNAME', password: 'PASSWORD' },
    },
}).then((response) => console.log('Exit IP:', response.data));
```

Runnable versions are in [examples/](examples/). For SOCKS5, use `--socks5-hostname` in cURL or a `socks5h://` proxy URL in Python.

## Country targeting

Mobile proxies target at the country level. You choose the country in the dashboard, generate credentials, then connect as above. Coverage spans 100+ countries on the rotating mobile line. Check the [locations page](https://www.proxy-cheap.com/locations) for the current list.

## Protocols and authentication

- **Protocols:** HTTP, HTTPS, and SOCKS5.
- **Authentication:** username and password, or IP whitelist where you register your server IP in the dashboard and skip per-request credentials.

## Pricing

Rotating mobile proxies bill pay-as-you-go by bandwidth, per GB, with no monthly commitment and no setup costs. Static mobile is priced per IP. See the [mobile proxies](https://www.proxy-cheap.com/services/mobile-proxies) page for current rates.

## FAQ

### What is a 4G mobile proxy?

A 4G mobile proxy routes traffic through an IP assigned by a mobile carrier to a device on its 4G network. The request carries a mobile carrier identity, which is the highest-trust profile among proxy types.

### What is the difference between rotating and static mobile proxies?

Rotating mobile proxies change the IP automatically per session from a carrier pool. Static mobile proxies hold one fixed IP for the subscription, with on-demand rotation available from the dashboard.

### Are 5G proxies faster than 4G?

Yes. 5G offers the highest throughput, 4G and LTE are the common fast choice, and 3G is the slowest legacy option. A 4G proxy is the practical default for most workloads.

### Do mobile proxies support SOCKS5?

Yes. Mobile proxies support HTTP, HTTPS, and SOCKS5. Use `socks5h` when you want the proxy to resolve DNS.

### How are mobile proxies priced?

Rotating mobile is pay-as-you-go by bandwidth, per GB, with no monthly commitment. Static mobile is per IP. Check the live product page for current pricing.

### Can I target a specific carrier?

Mobile proxies target at the country level. For carrier-specific targeting, the static residential (ISP) line supports ISP and carrier selection.

## Further reading

- [Proxy-Cheap mobile proxies](https://www.proxy-cheap.com/services/mobile-proxies)
- [Proxy-Cheap residential proxies](https://www.proxy-cheap.com/services/residential-proxies)
- [Proxy-Cheap locations](https://www.proxy-cheap.com/locations)
- [Proxy-Cheap support knowledge base](https://support.proxy-cheap.com)
- [Proxy-Cheap REST API documentation](https://docs.proxy-cheap.com)

## License

MIT

---

*This is a personal documentation repo, not an official Proxy-Cheap project. Connection examples use standard proxy configuration and work with any provider. Verify country coverage, carrier availability, and pricing on the live product page before relying on them.*
