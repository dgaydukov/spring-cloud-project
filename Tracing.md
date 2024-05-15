# Tracing

### Description
Tracing is the most useful feature for MS development. It helps you connect logs across multiple services using unique `tradeId` param. Moreover in case of error or any other unexpected behavior you can return this `tradeId` to end user, and if user contacts you, he would provide unique `traceId` by which you can identify the problem to this specific user.