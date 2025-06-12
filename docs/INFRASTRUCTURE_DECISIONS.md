# Infrastructure Decisions

## Hosting Platform
- Use **Hetzner VPS** for cost-effective and full-control hosting.
- Begin with a single VPS and scale to multiple VPS nodes for a multi-node Kubernetes cluster.

## Kubernetes Distribution
- Use **K3s** (lightweight Kubernetes) for easier installation and management on VPS.
- K3s includes Traefik as the default ingress controller.
- Optionally, customize Traefik installation using Helm for advanced features.

## Cluster Setup
- Initial setup on one VPS as the Kubernetes master (server).
- Additional VPS nodes join as worker nodes using K3s agent.
- Nodes communicate over private network or VPN for security and performance.

## DNS & Ingress
- Use Hetzner DNS or Cloudflare for DNS management.
- Create wildcard DNS entry (`*.yourapp.com`) pointing to the cluster ingress IP.
- Traefik handles routing based on subdomains.

## SSL Certificates
- Use Traefik’s integrated Let's Encrypt support to automatically provision and renew wildcard and individual certificates.

## Scaling & High Availability
- Scale horizontally by adding more VPS nodes to the cluster.
- Kubernetes distributes workloads across nodes for load balancing and failover.
- Regular backups of databases and Kubernetes manifests are mandatory.

## Security Considerations
- Secure cluster networking.
- Manage secrets using Kubernetes Secrets or external vault solutions.
- Harden VPS and Kubernetes configurations according to best practices.

---

## Future Considerations
- Move to managed database services (e.g., Amazon RDS) for easier maintenance.
- Consider managed Kubernetes services (e.g., AKS, EKS, GKE) if migrating to cloud.
- Implement GitOps workflows using ArgoCD or Flux.
