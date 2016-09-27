# Clusters

Clusters, also referred to as container cluster, is a group of hosts that are all capable of running containers together. Technically you can have a cluster of one host, but in production it tends to mean two or more hosts connected in a way where they can be utilized in unison.

The ability to run application code across many different environments is very beneficial for managing applications with high-load and large-resource usages. In enterprise environments, clusters are used to operate applications across many hosts to handle all of the traffic and resources their application demands.

## Why Clusters?

It can be wondered, why implement a whole cluster for an application and not just use many containers? Isn't the point of containers to allow for scalability and isolation? Yes, that is the point. However, while containers allow for applications to be broken into small pieces and easily deployed, these applications must be able to scale to meet demands and always be available. Clusters address these concerns and add many benefits:

* **Horizontal scaling**: Clusters make it very easy to scale horizontally by adding more capacity through a setting or similar means.
* **Helps allow for [microservices][microserves]**: Clusters allow us to break down applications into individual services that can be separately managed and scaled.
* **Self-healing systems**: Container management systems utilizing clusters can restart applications from failed machines onto working machines easily

[microserves]: https://en.wikipedia.org/wiki/Microservices
