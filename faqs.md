---
description: Frequently Asked Questions about Optic
---

# FAQs

## How is Optic different than OpenAPI? 

OpenAPI provides a human/machine-readable format for describing APIs. Having standards is great, but OpenAPI has proven itself hard to use correctly, and maintaining a 10k line YAML file isn't very developer-friendly. 

Optic aims to provide the same value as OpenAPI -- a human/machine-readable description of an API, but with an emphasis on making the tooling easy-to-use and developer-friendly. You can read more [about how we do that here](./). 

## Where does the data live? 

Optic creates a folder called `.api` in your repo and we encourage you to check that into Git. The development and testing proxies run locally or in your infrastructure and never sends data back to us over the network. 

## Does Optic work with OpenAPI? 

Optic can import OpenAPI 2 & 3 reasonably well and can export OpenAPI 3. Once teams add Optic, most stop manually writing the OpenAPI file manually. 

## What are some limitations of Optic? 

* JSON + text bodies are the only type supported right now
* Advanced support for Links, JSON API and Hypermedia controls has not been implemented 
* We currently only support describing one content-type per body.
* Map types are not supported
* Tuples are not supported 
* String formats are not supported. \(currently in development\)
* No support for GraphQL
* No support for gRPC

If one of these or something else you find is a blocker, open an issue [https://github.com/opticdev/optic/issues](https://github.com/opticdev/optic/issues). We will do our best to get it implemented quickly. For those that purchase a license for the Team Edition. 

## How do you pay the bills? 

Optic sells a Team Edition with features that help larger organizations with API Lifecycle Management and their Governance initiatives. We are backed by YCombinator and have raised a seed round. Today Optic is fully open source and will always offer a free version for the community. 

## How can I help? 

We have docs for that too! Please read the [How To Contribute Guide](open-source/how-to-contribute.md)

