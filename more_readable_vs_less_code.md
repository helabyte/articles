<p align="center">
  <img width="540" height="540" src="https://github.com/helabyte/articles/blob/main/resources/more_readable_less_code_small.jpg">
</p>


# Writing more readable VS. less code
Imagine you are supposed to implement an interface which is going to be responsible for calculating the amount of money which can be lend to an employee. Obviously it depends on some factors but let’s assume that these are our deciding factors:

- has the employee been hired for longer than two years?
- Has the employee a current debt?
- Has the employee had any outstanding performance in the last year?
- Is the employee older than 60? (Your mean boss tries to avoid lending money to an good old friend who has put more than 20 years sweat and blood into growing his company and soon is headed to retirement!)

Based on the answers to the above questions the employee would be eligible to get a loan for amount between 2 and 10 times of his monthly salary.

**But before getting our hands dirty I would invite you to answer one simple question:**
> why do we need methods/functions?  
I know there are tons of benefits and reasons for enclosing a chunk of code in form of a function but one good classic answer would be this one :
**We write methods in order to obey DIY (don’t repeat yourself) principle.**

Did you get the main point? Somebody talked about REPEAT! Let me make it clear once again: One good reason to write methods is to avoid writing repetitive functionality!  
with all these in place, now let's get our hands dirty…  
The fact that the concrete implementation is not what I’m looking for, I would tell you that if it was my task, I would end up with something like this:
```
public class LoanServiceImpl implements LoanService {

    private final static BigDecimal baseCoefficient = BigDecimal.valueOf(2);
    private final EmployeeService employeeService;

    public LoanServiceImpl(final EmployeeService employeeService) {
        this.employeeService = employeeService;
    }

    @Override
    public BigDecimal calculateLoan(@NotNull Long employeeNumber) {
        coefficient = baseCoefficient;
        Employee employee = employeeService.findByEmployeeNumber(employeeNumber);

        coefficient = isEmployeeHiredLongerThanOneYearAgo(employee) ? coefficient.plus(baseCoefficient) : coefficient;
        coefficient = hasEmployeeCurrentDebt(employee) ? coefficient.plus(baseCoefficient) : coefficient;
        coefficient = hasEmployeeOutstandingPerformanceInLastYear(employee) ? coefficient.plus(baseCoefficient) : coefficient;
        coefficient = isEmployeeOlderThanSixty(employee) ? coefficient.plus(baseCoefficient) : coefficient;

        return employee.getMonthlySalary.multiply(coefficient);
    }

    private boolean isEmployeeHiredLongerThanOneYearAgo(employee) {...}

    private boolean hasEmployeeCurrentDebt(employee) {...}

    private boolean hasEmployeeOutstandingPerformanceInLastYear(employee) {...}

    private boolean isEmployeeOlderThanSixty(employee) {...}
}

```
But wait a moment! didn't we agree, that we write methods to avoid having redundant chunk of functionality? Where is the need for repeatative code then? I mean as you see we called the private methods just once, so why should we bother ourslef to create all these four private methods?

The answer is, **please forget about this old stinky out of fashion belief which probably we learned in the first hour of "learning programming in one day" course!**  
>**You are almost always welcome to sacrifice writing less code in favor of having more readable code.**  

### FAQ: 

* But the methods are used just once!
    - So what?
* Now the methods are private, how can I write unit test for them?
    - You don't! You should assert the behavior of the `calculateLoan` method by mocking `EmployeeService`, how cool am I ? ):
* Why should I write more lines of code, while I could botch everything together and look more like a newbie?
    - Because you are caring more about looking like an experienced developer than having more readable and maintaniable code. 
   
