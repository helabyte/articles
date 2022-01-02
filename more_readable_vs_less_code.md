# writing Readable VS. Less

Imagine you are implementing an interface which is going to be responsible for calculating the amount of money which can be lend to an employee. Obviously it depends on some factors but let’s assume that these are our deciding factors:

- Is  the employee  hired for longer than two years?
- Has the employee a current debt?
- Has the employee any outstanding performance in last year?
- Is the employee older than 60?(Your mean boss tries to avoid lending money to an good old friend which has put more than 20 years sweat and blood in to growing his company and soon is head to retirement! )

with all these in place let's get our hands dirty…

For a long time, whenever I wanted to write some code I was asking my self, which one is better?
```
public class LoanServiceImpl implements LoanService {


    @Override
    public BigDecimal calculateLoan(Long employeeNumber) {

    }
}

```
