---
description: >-
  Helicone allows you to tag requests with any information you choose to
  segment, analyze, and visualize by
---

# Custom Properties

### What are Custom Properties?

Custom Properties allow you to add any additional information to your requests, such as:

* The **session**, **conversation**, or **app** id
* The **prompt chain** by adding a common value to group of requests
* **Application** or **user** metadata making the request

### Use Custom Properties to

* Get the the total cost or latency for a group of requests in a prompt chain
* Get the "unit economics" of your application, such as the average cost of a conversation or session
* Slice and dice your requests and metrics by any custom property

### Adding Custom Properties

Custom properties are added with headers to your OpenAI requests. For each header,

* The Key is `Helicone-Property-{Name}` with your property name in `Name`
* The Value is the string value for the property in the request.

{% tabs %}
{% tab title="Curl" %}
<pre><code>curl https://oai.hconeai.com/v1/completions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
<strong>  -H 'Helicone-Property-Session: "24"' \
</strong><strong>  -H 'Helicone-Property-Conversation: "support_issue_2"' \
</strong><strong>  -H 'Helicone-Property-App: "mobile"'
</strong>  -d ...
</code></pre>
{% endtab %}

{% tab title="Python" %}
<pre class="language-python"><code class="lang-python">openai.api_base = "https://oai.hconeai.com/v1"

openai.Completion.create(
    model="text-davinci-003",
    prompt="Say this is a test",
    headers={
<strong>        "Helicone-Property-Session": "24",
</strong><strong>        "Helicone-Property-Conversation": "support_issue_2",
</strong><strong>        "Helicone-Property-App": "mobile",
</strong>    }
)
</code></pre>
{% endtab %}

{% tab title="Node.js" %}
<pre class="language-typescript"><code class="lang-typescript">import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: "https://oai.hconeai.com/v1",
  baseOptions: {
    headers: {
<strong>      "Helicone-Property-Session": "24",
</strong><strong>      "Helicone-Property-Conversation": "support_issue_2",
</strong><strong>      "Helicone-Property-App": "mobile",
</strong>    },
  },
});
const openai = new OpenAIApi(configuration);
</code></pre>
{% endtab %}
{% endtabs %}
