# Internal management page acessible on public internet

Date: <todo><br/>
Classification: **Critical**<br/>
Source: `<todo: check if source wants public recognition>`<br/>
Payment: $600 (todo: double check this was the payment amount)<br/>

### Details

A security researcher doing a port scan of the internet found one of our internal management pages was publicly exposed (for nomad, a service orchestrator). This was a major issue and could have been really valuable to an attacker.

All internal secret keys were rotate and logs were audited to see if there had been any successful connection attempts from unknown IPs. There was no evidence of exploitation.

