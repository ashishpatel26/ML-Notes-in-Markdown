# Applications in Financial Services

## Traditional Sources

Traditionally, the following indicators have been used as data for finance:

1. Macro-Economic Indicators: GDP, Turnover etc.
2. Performance of investments over time: How well the stocks did?
3. Records of behavior of clients: If they paid on time or not

Although data science takes this a step further, because new sources can be now involved in the decision making process:

1. Unstructured text: Tweets, natural language records etc.
2. Sequence Data: How things change over time if sequence 1 is replaced with sequence 2.
3. Biometric markers: How 
4. Network data: Social relationships and insights into the records

## Decisions that need to be made

1. Acceptable level of risk
2. False positives and false negatives
3. Sources of your data: How reliable are these?
4. Importance of real-time analysis (because it would impact the range of algorithms that we can use)
5. Importance of interpretability

## Common ML Algorithms used with Financial Data

1. KNN
2. Regression
3. Decision Trees and RFs
4. ANNs
5. Deep Learning

## Potential Problems 

1. Flash crash: The process of having a large amount of change in the value of a security in very brief period of time is called a Flash Crash. The most recent one was when the value of Ethereum went from $319 to 10 cents in 2017<sup>[1](https://www.cnbc.com/2017/06/22/ethereum-price-crash-10-cents-gdax-exchange-after-multimillion-dollar-trade.html)</sup>.
2. Relevant data missing: The models are certainly not going to work if they have not been provided with all the information that is required to predict a particular value.
3. Overfitting
4. Black Box Models: It is very difficult to explain models that could give very impressive results to a non-technical person.
5. Unintentionally using restricted information: Things like race, gender etc. are often included in the application while training it, and are restricted in many countries from being used for any financial purposes because of racist biases that might creep in wuith them into the algorithm
