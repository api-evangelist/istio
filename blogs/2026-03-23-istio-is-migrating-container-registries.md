---
title: "Istio is Migrating Container Registries"
url: "https://istio.io/latest/blog/2026/retirement-of-gcr.io/"
date: "Mon, 23 Mar 2026 00:00:00 +0000"
author: ""
feed_url: "https://istio.io/latest/blog/feed.xml"
---
<p>Due to changes in Istio&rsquo;s funding model, Istio images will no longer be available at <code>gcr.io/istio-release</code> starting January 1st, 2027.
That is, clusters that reference images hosted on <code>gcr.io/istio-release</code> might fail to create new pods in 2027.</p>
<p>In fact, we are fully migrating all Istio artifacts out of Google Cloud, including Helm charts.
Future communications will cover the migration of Helm charts and other artifacts.
This post will focus on what you can do today in response to the 2027 container registry migration.</p>
<h2 id="am-i-affected">Am I affected?</h2>
<p>By default, Istio installations use Docker Hub (<code>docker.io/istio</code>) as their container registry, but many users choose to use the <code>gcr.io/istio-release</code> mirror.
You can check whether you are using the mirror using the following command.</p>
<pre><code class="language-bash">$ kubectl get pods --all-namespaces -o json \
    | jq -r '.items[] | select(.spec.containers[].image | startswith("gcr.io/istio-release")) | "\(.metadata.namespace)/\(.metadata.name)"'</code></pre>
<p>The above command will list all the pods that use images hosted on <code>gcr.io/istio-release</code>.
If there are any such pods, you will likely need to migrate.</p>
<div>
    <aside class="callout tip">
        <div class="type">
            <svg class="large-icon" xmlns="http://www.w3.org/2000/svg"><use xlink:href="/img/icons.svg#callout-tip" xmlns:xlink="http://www.w3.org/1999/xlink"></svg>
        </div>
        <div class="content">Even if you are using Docker Hub as your registry, we suggest that you migrate to <code>registry.istio.io</code> in case Istio images are no longer available on Docker Hub in the future.
See below for more details.</div>
    </aside>
</div>

<h2 id="what-to-do-today">What to do today</h2>
<p>Although we plan to keep images available on <code>gcr.io/istio-release</code> until late 2026,
we have set up <code>registry.istio.io</code> as the new home for Istio images.
Please migrate to using <code>registry.istio.io</code> as soon as possible.</p>
<h3 id="using-istioctl">Using <code>istioctl</code></h3>
<p>If you install Istio using <code>istioctl</code>, you can update your <code>IstioOperator</code> configuration as follows:</p>
<pre><code class="language-yaml"># istiooperator.yaml
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
spec:
  # ...
  hub: registry.istio.io/release
  # Everything else can stay the same unless you reference `gcr.io/istio-release` images elsewhere</code></pre>
<p>and install Istio using this configuration</p>
<pre><code class="language-bash">$ istioctl install -f istiooperator.yaml</code></pre>
<p>Alternatively, you can pass in the registry as a command line argument</p>
<pre><code class="language-bash">$ istioctl install --set hub=registry.istio.io/release # the rest of your arguments</code></pre>
<h3 id="using-helm">Using Helm</h3>
<p>If you use Helm to install Istio, update your values file to have the following:</p>
<pre><code class="language-yaml"># ...
hub: registry.istio.io/release
global:
  hub: registry.istio.io/release
# Everything else can stay the same unless you reference `gcr.io/istio-release` images elsewhere</code></pre>
<p>Then, update your Helm installation with your new values file.</p>
<h3 id="private-mirrors">Private mirrors</h3>
<p>Your organization might pull images from <code>gcr.io/istio-release</code>, push them to a private registry, and reference the private registry in your Istio installation.
This process will still work, but you will have to pull from <code>registry.istio.io/release</code> instead of <code>gcr.io/istio-release</code>.</p>
