---
title: Concepts
pcx-content-type: concept
weight: 2
layout: single
meta:
  title: Concepts
---

# Concepts

The Cloudflare Web Application Firewall (Cloudflare WAF) checks incoming web requests and filters undesired traffic based on sets of rules called rulesets. The matching engine that powers the WAF rules supports the wirefilter syntax using the [Rules language](/ruleset-engine/rules-language/).

{{<Aside type="note" header="What is a Web Application Firewall?">}}

A Web Application Firewall or WAF creates a shield between a web app and the Internet. This shield can help mitigate many common attacks. For a more thorough definition, refer to [Web Application Firewall explained](https://www.cloudflare.com/learning/ddos/glossary/web-application-firewall-waf/) in the Learning Center.

{{</Aside>}}

---

## Managed Rulesets

The Cloudflare WAF includes [several Managed Rulesets](/waf/managed-rulesets/), provided by Cloudflare, that you can enable and configure.

When you enable these Managed Rulesets, you get immediate protection from a broad set of security rules that are regularly updated. Each of these rules has a default action that varies according to the severity of the rule.

You can override the default action or disable one or more rules included in Managed Rulesets. To customize the rules behavior you define specific **configurations** or **overrides**.

You can define a configuration that affects an entire Managed Ruleset, or configure the action and status of one or more rules in the ruleset. Rules have associated **tags** that allow you to search for a specific group of rules and configure them in bulk.

## Custom rulesets

{{<Aside type="warning">}}

Currently, you can only create and deploy custom rulesets via API.

{{</Aside>}}

You can [create custom rulesets](/ruleset-engine/custom-rulesets/create-custom-ruleset/) with your own WAF rules that you can later [deploy to a phase entry point](/waf/managed-rulesets/deploy-api/#deploying-custom-rulesets).

## Available phases

The Web Application Firewall provides the following [phases](/ruleset-engine/about/phases/) where you can deploy WAF rules:

- `http_request_firewall_custom`
- `http_request_firewall_managed`

These phases exist both at the account level and at the zone level. Considering the available phases and the two different levels, the WAF rules are evaluated in the following order:

1.  Rules in the `http_request_firewall_custom` phase at the **account** level
2.  Rules in the `http_request_firewall_custom` phase at the **zone** level
3.  Rules in the `http_request_firewall_managed` phase at **account** level
4.  Rules in the `http_request_firewall_managed` phase at the **zone** level

## Deploying rulesets to phases

You can **deploy** the Managed Rulesets provided by WAF to the following phases:

- `http_request_firewall_managed` phase at the **account** level (the phase `kind` is `root`)
- `http_request_firewall_managed` phase at the **zone** level (the phase `kind` is `zone`)

{{<Aside type="note" header="Note">}}

When you deploy a Managed Ruleset in the dashboard in **Security** > **WAF** > **Managed rules**, you are deploying that ruleset to the `http_request_firewall_managed` phase of the selected zone.

When you deploy a Managed Ruleset using **Firewall Rulesets** in the dashboard at the account level, you are deploying that ruleset to the `http_request_firewall_managed` phase of the account.

{{</Aside>}}

To deploy your own WAF rules, create a custom ruleset and add any custom rules to this ruleset. Next, deploy the custom ruleset to a supported phase.

You can **create** and **deploy** custom rulesets to the `http_request_firewall_custom` phase at the **account** level (the phase `kind` is `root`).

{{<Aside type="warning">}}

Currently, creating and deploying custom rulesets is only available via API.

{{</Aside>}}

To learn more about phases, refer to [Phases](/ruleset-engine/about/phases/) in the Ruleset Engine documentation.

## Rule execution order

Cloudflare evaluates different types of rules when processing incoming requests. The rule execution order is the following:

* [Firewall rules](/firewall/cf-firewall-rules/), available in **Security** > **WAF** > **Firewall rules**
* [Custom rules](/waf/custom-rules/), available in **Security** > **WAF** > **Custom rules**
* [Rate limiting rules](/waf/rate-limiting-rules/), available in **Security** > **WAF** > **Rate limiting rules**
* [Managed Rulesets](/waf/managed-rulesets/), available in **Security** > **WAF** > **Managed rules**
* [Cloudflare Rate Limiting](https://support.cloudflare.com/hc/articles/115001635128) (previous version), available in **Security** > **WAF** > **Rate limiting rules**
