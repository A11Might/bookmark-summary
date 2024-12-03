# WireGuard at Modal: Static IPs for Serverless Containers
- URL: https://modal.com/blog/vprox
- Added At: 2024-12-03 00:28:33
- [Link To Text](2024-12-03-wireguard-at-modal-static-ips-for-serverless-containers_raw.md)

## TL;DR
Modal通过基于Go和WireGuard的VPN代理_vprox_，解决了无服务器计算中动态IP访问特定IP列表服务的问题。该代理在第3层运行，确保多个容器出站流量的源IP一致性，并通过策略路由和动态IP管理优化网络性能。Modal已开源相关实现，并欢迎开发者加入团队。

## Summary
1. **概述**：
   - Modal构建了一个基于Go的高可用VPN代理，名为_vprox_，使用WireGuard实现。
   - 该代理在网络堆栈的第3层（IP层）运行，允许将全球容器中的出站流量通过静态IPv4地址进行路由。

2. **场景描述**：
   - 2024年，用户选择无服务器云平台时，发现Modal。通过简单的Python函数和`modal deploy`命令，即可在云中快速部署cron作业和API端点。
   - Modal函数在全球多个云提供商的数十个区域运行，优化计算价格并动态扩展以满足需求。

3. **问题引入**：
   - 用户希望将无服务器函数连接到需要特定IP访问列表的MongoDB云数据库，但传统方法无法满足无服务器计算的动态IP需求。

4. **解决方案**：
   - **静态出站IP需求**：通过代理实现静态IP，解耦IP地址与实际计算资源。
   - **SOCKS5代理**：最初尝试使用SOCKS5代理，但存在API不明显和用户需手动配置的问题。
   - **WireGuard引入**：在第3层（IP层）使用WireGuard VPN，确保多个容器出站流量的源IP一致性。

5. **WireGuard实现**：
   - **WireGuard网络设置**：在代理服务器和Modal工作节点之间建立WireGuard网络，配置流量路由。
   - **客户端连接管理**：客户端定期检查VPN连接，失败时自动重连。

6. **网络策略路由**：
   - **容器网络命名空间**：每个容器有自己的网络命名空间和虚拟以太网接口（veth），通过桥接设备和IP伪装（SNAT）实现出站流量路由。
   - **策略路由规则**：通过策略路由，将特定容器的流量路由到指定的WireGuard接口，解决Linux路由表不支持按源IP路由的问题。

7. **代理服务器优化**：
   - **多IP分配**：每个代理服务器分配多个IP，提高资源利用率。
   - **动态IP管理**：通过代码自动检测和重新配置IP地址，实现高可用性和故障恢复。

8. **技术细节**：
   - **rp_filter设置**：在不同Linux发行版上测试时，发现需要调整`rp_filter`设置以确保WireGuard正常工作。

9. **使用与开源**：
   - **开发者使用**：Modal开发者可通过Team计划访问静态IP代理功能。
   - **开源项目**：Modal开源了WireGuard控制平面实现，可在GitHub上找到。

10. **总结与招聘**：
    - Modal团队对静态IP项目感到兴奋，并感谢团队成员的贡献。
    - Modal正在招聘，欢迎有兴趣构建可靠、安全系统的工程师加入。
