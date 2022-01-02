# Writing more readable VS. less code

Imagine you are supposed to implement an interface which is going to be responsible for calculating the amount of money which can be lend to an employee. Obviously it depends on some factors but let’s assume that these are our deciding factors:

- Is the employee  hired for longer than two years?
- Has the employee a current debt?
- Has the employee any outstanding performance in last year?
- Is the employee older than 60?(Your mean boss tries to avoid lending money to an good old friend which has put more than 20 years sweat and blood in to growing his company and soon is head to retirement!)

Based on the answers to the above questions the employee would be eligible to get a loan for something in amount of 2-10 times of his monthly salary.

**But before getting our hands dirty I would invite you to answer one simple question:**
> why do we need methods/functions?  
I know there are tones of benefits and reasons for enclosing a chunk of code in form of a function but  one good classic answer would be this one :
**We write methods in order to obey DIY (don’t repeat yourself) principle.**

Did you get the main point? Somebody talked about REPEAT! Let me make it clear once again, One good reason to write methods is to avoid writing repetitive functionality!  
with all these in place, now let's get our hands dirty…  
The fact that the concrete implementation is not what I’m looking for, I would tell you that if It was my task, I would end up with something like these :
```
public class LoanServiceImpl implements LoanService {

    final BigDecimal baseCoefficient = 2;

    @Autowired
    private final EmployeeService employeeService;

    @Override
    public BigDecimal calculateLoan(@NotNull Long employeeNumber) {
        Employee employee = employeeService.findByEmployeeNumber(employeeNumber);

        baseCoefficient = isEmployeeHiredLongerThanOneYearAgo(employee) ? baseCoefficient + 2 : baseCoefficient;
        baseCoefficient = hasEmployeeCurrentDebt(employee) ? baseCoefficient + 2 : baseCoefficient;
        baseCoefficient = hasEmployeeCurrentDebt(employee) ? baseCoefficient + 2 : baseCoefficient;
        baseCoefficient = isEmployeeOlderThanSixty(employee) ? baseCoefficient + 2 : baseCoefficient;

        return employee.getMonthlySalary.multiply(baseCoefficient);

    }

    private boolean isEmployeeHiredLongerThanOneYearAgo(employee){...}

    private boolean hasEmployeeCurrentDebt(employee){...}

    private boolean hasEmployeeCurrentDebt(employee){...}

    private boolean isEmployeeOlderThanSixty(employee){...}
}

```
