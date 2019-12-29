---
description: Learn how to set up Optic in your development environment.
---

# Quick Start

## Overview

Optic is the developer-friendly alternative to manual OpenAPI workflows. It's sort of like Git, but for managing changes to your API contract. ‌ 

The open-source tool monitors the behavior of your APIs compares it to you API spec. Optic logs instances where the API does not follow the spec and gives you the option to a\) automatically update the spec, or b\) mark the behavior as a bug in your issue tracker.

#### What does Optic replace? 

* Your `generate-swagger-from-code` library with a more accurate tool that does not require leaving ugly annotations throughout your code. 
* Manually writing an OpenAPI spec and remembering to update it every time you change the API
* Writing contract tests. Optic detects when you break your API's contract and can even be set up to sample traffic in staging, pre-prod, and production environments. 
* Your internal API docs \(SwaggerUI\) with beautiful Stripe-like API docs

## What do I have to do to set it up? 

The quickest way to try Optic is to run it locally. Setting it up will take you less than 5 minutes. 

1. Install the Optic CLI
2. Tell Optic how to start your API server i.e. `rails server` 
3. Use Optic's `api start` command to start your API. This wraps your server in the local Optic proxy so it can watch how your API behaves. 

### Install the Optic CLI

{% tabs %}
{% tab title="yarn" %}
```bash
$ yarn add global @useoptic/cli
```
{% endtab %}

{% tab title="npm" %}
```
$ npm install @useoptic/cli -g
```
{% endtab %}
{% endtabs %}

### Tell Optic how to Start your API

Optic provides the `api start` command which:

1. Starts your API on a random port
2. Starts an Optic monitoring proxy configured to route traffic from your preferred port to the underlying API

{% hint style="info" %}
So if you have a Rails API that you usually run on port `4005`, Optic's `api start` command will start the API on a random port like `6554` and route traffic through `4005` to `6554` -- the only difference as far as you're concerned is that Optic sits in the middle. 
{% endhint %}

#### Run \`api init\` from your API's directory 

Optic will ask you a series 3 quick questions -- here's how you should answer them. 

```bash
cd /path/to/api
api init

API Name: my-api           # Name your API
Port: 4005                 # The port your API runs on locally today
Command to start API: ___  # See Below 

```

Use the command from the table below. If you don't see your framework listed press "Other"

{% tabs %}
{% tab title="Express" %}
**Command:** Use the command you use to start your API today. ie `npm run start` or `node server.js`

**Code changes:** Optic needs the ability to assign your API a port when you're running `api start`. Read the port from the `OPTIC_API_PORT` environment variable. 

```javascript
# before 
app.listen(process.env.PORT || 3000)
# after
app.listen(process.env.OPTIC_API_PORT || process.env.PORT || 3000)
```
{% endtab %}

{% tab title="Rails" %}
**Command:** Use the `rails server` command with the port argument set to Optic's environment variable. 

```bash
rails server -p \$OPTIC_API_PORT
```
{% endtab %}

{% tab title="Laravel" %}
**Command:** Use the `artisan serve` command with the port argument set to Optic's environment variable. 

```bash
php artisan serve --port=\$OPTIC_API_PORT
```
{% endtab %}

{% tab title="CodeIgniter " %}
**Command:** Use the `spark serve` command with the port argument set to Optic's environment variable. 

```bash
php spark serve --port=\$OPTIC_API_PORT
```
{% endtab %}

{% tab title="Flask" %}
**Command:** Use the `flask run` command with the port argument set to Optic's environment variable. 

```bash
flask run --host=0.0.0.0 --port=\$OPTIC_API_PORT
```
{% endtab %}

{% tab title="Play" %}
**Command:** Use the `sbt run` command with the port argument set to Optic's environment variable. 

```bash
sbt \"run -Dhttp.port=\$OPTIC_API_PORT\"
```
{% endtab %}

{% tab title="Zeit Now" %}
**Command:** Use the `now dev` command with the port argument set to Optic's environment variable. 

```
now dev --listen \$OPTIC_API_PORT
```
{% endtab %}

{% tab title="Other" %}
**We're sorry we don't have docs for your framework!**  
  
For the command, use whatever command you usually use to start your server. The one thing you have to change in either your code or the command is the port.   
  
Optic needs the ability to start your API on a port of its choosing. It will inject the port as an environment variable called `OPTIC_API_PORT`. Whenever that environment variable is present, your API should read from it and start itself listening on that port.   
  
If you need help getting it setup [click here to schedule a quick call with an Optic maintainer](https://calendly.com/optic-onboarding/setup-help). 

{% embed url="https://adc2019.typeform.com/to/bof781" %}
{% endtab %}
{% endtabs %}

After you answer all of Optic's questions, it adds a `.api` folder in your API repo. This folder stores the API specification that Optic maintains for you, a config file with the information you supplied, and example requests / responses for your API documentation.

{% hint style="warning" %}
If you run your API locally on a custom host ie `api.local` you will also need to edit the config file Optic writes to `.api/api.yml`  
make `target: 'http://your-custom.host:{{ENV.OPTIC_API_PORT}}'`
{% endhint %}

### Run your API with \`api start\`

Let's make sure everything is working! Run Optic's start command:

```bash
api start
```

Send some traffic to your API! If the API responds Optic is set up!

If it didn't work, set up a quick call and we will help you get things working:

{% embed url="https://calendly.com/optic-onboarding/setup-help" %}

