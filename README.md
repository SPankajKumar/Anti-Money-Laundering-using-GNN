# Anti-Money-Laundering-using-GNN



Anti-Money Laundering Using Graph Neural Networks
							

Pankajkumar S,21BCE1655
					



Abstract
Money laundering is a complex global issue where criminals disguise illegal funds as legitimate income. Traditional Anti-Money Laundering (AML) systems struggle to adapt to the increasingly sophisticated laundering techniques that evade detection. With the vast amount of transaction data available, there is a need for more advanced techniques to detect suspicious activity. In this paper, we propose a Graph Neural Network (GNN) approach for detecting money laundering activities by analyzing the transactional network of entities. GNNs leverage the relational structure of the data, allowing them to capture complex interactions between entities. We outline the model's architecture, focusing on the importance of feature selection for nodes and edges in the transactional graph. Addressing data imbalance (only 0.0021% of transactions are laundering-related), we employ oversampling techniques to improve the performance. Our results demonstrate the efficacy of GNNs over traditional methods, achieving better detection of suspicious activities in the financial system.



Introduction

Money laundering poses a severe threat to the global financial system, allowing criminals to convert illicit gains into seemingly legitimate assets. This process not only threatens the integrity of financial institutions but also enables the financing of criminal activities, including terrorism and corruption. Despite the extensive efforts made by financial regulators and institutions worldwide, detecting and preventing money laundering remains a challenging task due to the ever-evolving strategies used by criminals to circumvent detection.

Traditional Anti-Money Laundering (AML) techniques often rely on rule-based systems or machine learning algorithms. Rule-based systems are static and require continuous updating to adapt to new laundering strategies, whereas conventional machine learning models, while more flexible, often fail to capture the intricate relationships between entities within a network of transactions. This limitation makes it difficult to detect complex laundering schemes that exploit transactional networks over time.

To address these shortcomings, we propose using Graph Neural Networks (GNNs) to model the transactional relationships between entities in a financial network. GNNs can learn from graph-structured data by considering both the entities (nodes) and the interactions between them (edges), making them well-suited for fraud detection tasks. This paper presents a novel GNN-based approach for identifying suspicious transactions within large-scale financial networks, leveraging the transactional and entity-level features for effective money laundering detection.



Background

In a typical financial transaction system, each entity, such as an individual or an organization, is involved in multiple transactions that can be represented as a graph. In this context:
- Nodes: represent entities (e.g., senders and receivers of funds).
- Edges: represent transactions between entities, containing attributes like transaction amount, currency, and payment method.

Graph-based representations of transactional data allow for deeper insights into the relationships between entities. For example, an individual may be involved in multiple transactions across different accounts, and understanding these interactions could reveal suspicious patterns that would otherwise be missed by traditional approaches.

Graph Neural Networks
GNNs are particularly effective in modeling such relationships. By learning node representations that aggregate information from neighboring nodes (connected entities), GNNs can effectively capture the structure and properties of the entire graph. This approach allows for enhanced detection of suspicious activities within the transactional network.



Methodology

In this section, we explain the design of the GNN model for detecting money laundering, including the handling of node and edge features, and the purpose of oversampling due to data imbalance.

 Graph Construction

In the proposed GNN framework, the transactional data is represented as a graph \( G = (V, E) \), where \( V \) is the set of nodes (entities) and \( E \) is the set of edges (transactions). Each entity (node) is connected to other entities through transactional edges, and these relationships are used to infer whether a given entity is involved in suspicious activity.

- Nodes (Entities): Each node represents an entity, such as a sender or receiver. The node features include attributes such as the total amount sent/received, the banks involved, and the currencies used.
- Edges (Transactions): An edge between two nodes represents a transaction between them, with features like the transaction amount, payment currency, and the banks facilitating the transfer.

 Feature Extraction

Node Features:
Node features capture the behavior of entities participating in transactions. In our model:
- We extract features like the total amount of money paid (`Amount_Paid`) and received (`Amount_Received`) by an entity.
- Categorical features such as the banks involved (`From_Bank`, `To_Bank`) and the currencies used (`Payment_Currency`, `Receiving_Currency`) are label-encoded into numerical values.


Edge Features:
Edge features describe the transactional details between nodes:
- Transaction amount (`Amount Paid`).
- Payment currency and receiving currency.
- Transaction method (`Payment_Format`).

These features represent the details of each transaction and help in determining whether the transaction is suspicious.

GNN Model Architecture

Our GNN model leverages graph convolution layers to learn from the graph-structured data. The key components of the model include:

- GCNConv Layers: Two graph convolution layers (`GCNConv`) are used to aggregate information from neighboring nodes. These layers help the model understand the relational structure of the graph.
- Activation Functions: We apply the ReLU activation function to introduce non-linearity into the model after each convolution operation.
- Global Pooling: The `global_mean_pool` function is used to combine node-level features into a graph-level representation, allowing for the classification of the graph (transaction network) as money laundering or not.

Handling Data Imbalance (Oversampling)

One of the significant challenges in this task is the severe class imbalance: only 0.0021% of the transactions are labeled as laundering. Without addressing this imbalance, the model would be biased towards predicting non-laundering transactions, leading to artificially high accuracy.

To mitigate this, we apply oversampling techniques to balance the training dataset. Oversampling increases the number of laundering samples, improving the model's ability to learn the patterns of suspicious transactions.

This ensures that the model is trained on a balanced dataset, enhancing its ability to detect money laundering effectively.



Implementation

The implementation is done using PyTorch Geometric, a framework for deep learning on graphs. The key steps include:

1. Data Preprocessing: We preprocess the data by extracting and encoding node and edge features.
2. Graph Construction: A graph is constructed using PyTorch Geometric’s `Data` class, representing the transactional network.
3. Model Training: The GNN model is trained using the Adam optimizer and cross-entropy loss, with the target being the label indicating whether a transaction is part of money laundering activity.



Results

The GNN model achieved high performance in detecting suspicious transactions. After applying oversampling techniques, the model's precision, recall, and F1-score improved significantly. Compared to traditional machine learning approaches, the GNN model showed superior ability to capture complex relationships between entities, making it more effective for money laundering detection.



Conclusion

This paper presented a novel approach using Graph Neural Networks (GNNs) for anti-money laundering detection. By leveraging the relationships between entities in a transactional network, GNNs can detect complex laundering schemes that traditional approaches may miss. Future work could focus on improving the scalability of the model to larger datasets and integrating real-time detection mechanisms.



References
- Kipf, T. N., & Welling, M. (2017). Semi-Supervised Classification with Graph Convolutional Networks. ICLR 2017.
- Wang, Y., Wang, X., & He, X. (2019). Neural Graph Collaborative Filtering. In Proceedings of the 42nd International ACM SIGIR Conference.
- Wu, Z., Pan, S., Chen, F., Long, G., Zhang, C., & Yu, P. S. (2020). A Comprehensive Survey on Graph Neural Networks. IEEE Transactions on Neural Networks and Learning Systems.


