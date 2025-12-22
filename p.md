# Tôi cần thiết kế cho project này là 1 chatbot agent với các chức năng và yêu cầu sau:

1. Yêu cầu:
   Đây là 1 chatbot sử dụng các cơ chế RA, Agentic RAG để build 1 chatbot agent có khả năng giao tiếp với user
   Tôi muốn sử dụng mongoDB để lưu trữ vector embeded database
   chatbot là chat về nhiều vấn đề khác nhau tuỳ theo user muốn. trước tiến sẽ làm về chơi đoán từ. sau này sẽ mở rộng ra các chức năng khác.
   Đối với chơi đoán từ: đây sẽ user sẽ đóng vài người đưa ra các mô tả và agent chịu trách nhiệm đoán xem user đang nói đến còn vật gì, đồ vật gì. hoặc ngược lại. user đóng vai ngừoi doán, agent đóng vài người đưa ra mô tả. trong qua trình ngừoi đưa ra mô tả, người đoán có thể hỏi ngược lại. ví dụ:
   - user: 1 thức có 3 chân
   - agent: nó là con vật hay là đồ vật?
   - user: nó là đồ vật
   - agent: cái bàn đúng không?
   - user: không, nó dùng để ngồi
   - agent: à, nó là cái ghế đúng không?
   - user: đúng
2. nếu user hỏi những câu hỏi không liên quan đến các chức năng đang có của agent. ví dụ agent chỉ có chức năng chơi đoán từ. thì cần từ chối vì nằm ngoài khả năng của angent. nếu user cứ liên tục phớt lờ mà yêu cầu ngoài phạm vi thì trả lời bằng giọng điệu khó chịu, bỗ bã không kiêng nể. ngôn ngữ giao tiếp.tránh văn vở
3. Cần vẽ flow mermaid chart bao gồm flow implement vector database, flow implement agent, flow implement chatbot,... để tôi nắm review tổng thể các phần xương sống cần làm
