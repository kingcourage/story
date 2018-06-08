首先需要注入事物管理的bean

``` stylus
@Autowired
private DataSourceTransactionManager transactionManager;
```
然后开启写自己的业务代码，提交事物

``` stylus
DefaultTransactionDefinition def = new DefaultTransactionDefinition();
def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRES_NEW); // 事物隔离级别，开启新事务，这样会比较安全些。
TransactionStatus status = transactionManager.getTransaction(def); // 获得事务状态
try {
	//逻辑代码，可以写上你的逻辑处理代码
	transactionManager.commit(status);
} catch (Exception e) {
	transactionManager.rollback(status);
}
```


