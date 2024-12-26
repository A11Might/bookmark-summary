# Server-Sent Events (SSE) Are Underrated
- URL: https://igorstechnoclub.com/server-sent-events-sse-are-underrated/
- Added At: 2024-12-26 00:28:53
- [Link To Text](2024-12-26-server-sent-events-(sse)-are-underrated_raw.md)

## TL;DR
Server-Sent Events (SSE) 是一种基于HTTP的单向通信技术，适合服务器向客户端推送实时更新。其优势在于实现简单、资源效率高、自动重连以及与现有基础设施兼容。尽管SSE在双向通信上不如WebSocket，但在实时新闻、股票行情、任务监控等单向数据流场景中表现优异。SSE在现代浏览器中广泛支持，是实时通信的优雅解决方案。

## Summary
1. **SSE简介**：Server-Sent Events (SSE) 是一种从服务器到客户端的单向通信技术，基于HTTP协议，适合服务器向客户端推送实时更新。

2. **SSE被低估的原因**：
   - **WebSocket的流行**：WebSocket的双向通信能力使得SSE的单向通信显得不够突出。
   - **感知到的限制**：SSE的单向性可能被认为限制了其应用场景，尽管它在许多情况下已经足够。

3. **SSE的关键优势**：
   - **实现简单**：SSE基于标准HTTP协议，避免了WebSocket连接管理的复杂性。
   - **基础设施兼容性**：SSE与现有的HTTP基础设施（如负载均衡器、代理、防火墙）无缝兼容。
   - **资源效率**：由于单向通信和标准HTTP连接的使用，SSE的资源消耗较低。
   - **自动重连**：浏览器内置支持连接中断处理和自动重连，提供稳定的实时体验。
   - **清晰的语义**：单向通信模式使得数据流清晰，应用逻辑简化。

4. **实际应用场景**：
   - 实时新闻推送和社交更新
   - 股票行情和金融数据
   - 进度条和任务监控
   - 服务器日志流
   - 协作编辑（用于更新）
   - 游戏排行榜
   - 位置跟踪系统

5. **实现示例**：
   - **服务器端（Flask）**：
     ```python
     from flask import Flask, Response, stream_with_context
     import time
     import random

     app = Flask(__name__)

     def generate_random_data():
         while True:
             data = f"data: Random value: {random.randint(1, 100)}\n\n"
             yield data
             time.sleep(1)

     @app.route('/stream')
     def stream():
         return Response(
             stream_with_context(generate_random_data()),
             mimetype='text/event-stream'
         )

     if __name__ == '__main__':
         app.run(debug=True)
     ```
   - **客户端（JavaScript）**：
     ```javascript
     const eventSource = new EventSource("/stream");

     eventSource.onmessage = function(event) {
         const dataDiv = document.getElementById("data");
         dataDiv.innerHTML += `<p>${event.data}</p>`;
     };

     eventSource.onerror = function(error) {
         console.error("SSE error:", error);
     };
     ```

6. **代码解释**：
   - **服务器端组件**：
     - `/stream` 路由处理SSE连接。
     - `generate_random_data()` 持续生成格式化的事件。
     - `text/event-stream` MIME类型标识SSE协议。
     - `stream_with_context` 维护Flask应用上下文。
   - **客户端组件**：
     - `EventSource` 对象管理SSE连接。
     - `onmessage` 处理程序处理传入事件。
     - `onerror` 处理连接问题。
     - 浏览器自动处理重连。

7. **限制与注意事项**：
   - **单向通信**：仅支持服务器到客户端的通信，客户端到服务器的通信需要单独的HTTP请求。
   - **浏览器支持**：现代浏览器广泛支持，但旧版浏览器可能需要polyfill。
   - **数据格式**：主要支持文本数据，二进制数据需要编码（如Base64）。

8. **最佳实践**：
   - **错误处理**：
     ```javascript
     eventSource.onerror = function(error) {
         if (eventSource.readyState === EventSource.CLOSED) {
             console.log("Connection was closed");
         }
     };
     ```
   - **连接管理**：
     ```javascript
     function closeConnection() {
         eventSource.close();
     }
     ```
   - **重连策略**：
     ```javascript
     let retryAttempts = 0;
     const maxRetries = 5;

     eventSource.onclose = function() {
         if (retryAttempts < maxRetries) {
             setTimeout(() => {
                 // Reconnect logic
                 retryAttempts++;
             }, 1000 * retryAttempts);
         }
     };
     ```

9. **现实世界示例：ChatGPT的实现**：
   - **通用模式**：所有主要LLM提供商使用SSE进行流式响应，返回`content-type: text/event-stream`头，数据块以`\r\n\r\n`分隔，每个块包含`data: JSON`行。
   - **OpenAI实现**：
     - **请求结构**：
       ```bash
       curl https://api.openai.com/v1/chat/completions \
         -H "Content-Type: application/json" \
         -H "Authorization: Bearer $OPENAI_API_KEY" \
         -d '{
           "model": "gpt-4o-mini",
           "messages": [{"role": "user", "content": "Hello, world?"}],
           "stream": true,
           "stream_options": {
             "include_usage": true
           }
         }'
       ```
     - **响应格式**：每个数据块包含模型、选择、使用情况等信息。
     - **关键头信息**：包括速率限制、处理时间等。

10. **结论**：SSE为实时、服务器到客户端的通信提供了一个优雅的解决方案。其简单性、效率以及与现有基础设施的集成使其成为许多应用的优秀选择。尽管WebSocket在双向通信中仍然有价值，SSE在单向数据流场景中提供了更专注且更合适的解决方案。
