# Backend Interview Question Bank — Java + Spring Boot

Use these as active-recall prompts.

Do not memorize one-line answers. Explain with examples.

# Java

1. How does HashMap work at a high level?
2. ArrayList vs LinkedList?
3. HashMap vs ConcurrentHashMap?
4. equals vs hashCode?
5. checked vs unchecked exception?
6. Optional best practices?
7. record vs class?
8. StringBuilder vs StringBuffer?
9. immutable object requirements?
10. map vs flatMap?

# OOP / SOLID

11. inheritance vs composition?
12. explain SRP with a bad class example.
13. explain OCP with a payment example.
14. explain DIP in Spring.
15. can SOLID be overused?
16. interface vs abstract class?
17. anemic domain model?
18. what should a controller do?
19. what should a service do?
20. entity vs DTO?

# Concurrency

21. race condition?
22. atomicity?
23. visibility?
24. volatile vs synchronized?
25. synchronized vs Lock?
26. AtomicInteger use cases?
27. thread-safe collection examples?
28. CompletableFuture?
29. virtual threads?
30. why must singleton Spring services usually be stateless?

# Spring

31. Spring vs Spring Boot?
32. IoC?
33. DI?
34. constructor injection?
35. bean lifecycle?
36. bean scope?
37. component scanning?
38. auto-configuration?
39. profiles?
40. configuration properties?

# REST

41. PUT vs PATCH?
42. 401 vs 403?
43. 400 vs 422?
44. pagination approaches?
45. idempotent HTTP methods?
46. API versioning?
47. global exception handling?
48. correlation ID?
49. why not return entities directly?
50. how would you design an order cancel operation?

# Database

51. transaction?
52. isolation?
53. optimistic vs pessimistic locking?
54. N+1?
55. lazy vs eager?
56. index?
57. composite index?
58. why do DB constraints matter?
59. what is deadlock?
60. how would you prevent overselling inventory?

# Messaging

61. RabbitMQ vs Kafka?
62. queue vs topic?
63. consumer group?
64. at-most-once vs at-least-once?
65. duplicate delivery?
66. DLQ?
67. retry strategy?
68. backpressure?
69. outbox pattern?
70. how do you make a consumer idempotent?

# Caching

71. local vs distributed cache?
72. cache-aside?
73. TTL?
74. cache invalidation?
75. cache stampede?
76. stale data?
77. Redis failure behavior?
78. Caffeine use case?
79. what should not be cached?
80. cache hit ratio?

# Idempotency

81. what is idempotency?
82. why is payment creation risky?
83. idempotency key?
84. request fingerprint?
85. DB uniqueness?
86. duplicate event deduplication?
87. retry after timeout?
88. same key with different body?
89. idempotency retention period?
90. transaction boundary around dedupe?

# Security

91. authentication vs authorization?
92. TLS?
93. mTLS?
94. JWT?
95. is JWT encrypted?
96. JWT claims?
97. OAuth2?
98. OIDC?
99. access vs refresh token?
100. CORS vs CSRF?

# Patterns

101. Strategy?
102. Factory?
103. Decorator?
104. Singleton?
105. Observer?
106. Adapter?
107. Template Method?
108. Proxy?
109. which patterns does Spring use?
110. when should you avoid a pattern?

# Testing

111. unit vs integration?
112. mock vs stub?
113. what should be mocked?
114. test pyramid?
115. Testcontainers?
116. TDD?
117. Red/Green/Refactor?
118. brittle test?
119. contract testing?
120. how would you test async messaging?

# Production

121. logs vs metrics vs traces?
122. readiness vs liveness?
123. timeout vs retry?
124. retry storm?
125. connection pool?
126. memory leak vs allocation pressure?
127. horizontal scaling?
128. what happens during rolling deployment?
129. how would you debug a slow API?
130. what would you monitor on a message consumer?
