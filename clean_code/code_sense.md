# CLEAN CODE


## BAD CODE

* Aggressive release cycles, quick product to market movement should be accompanies with careful consideration on code. Companies are brought down by poor code
* Impeding caused by bad code is called wading
* We all think of going back and cleaning it later -
> LeBlanc's Law: "Later equals never"

### Total Cost of Owning a Mess

* As mess builds, productivity of team continues to asymptotically reduce to zero
* As productivity decreases, management does the following:
    * Add more staffs to project
        - New Staffs with the messy code, do not understand the changes which match the design intent and ones which thwarts the design intent.
        - Under pressure to increase producitvity of project, they succumb to creating more messy code.
        - This drives productivity even below zero.

## What next? 

### Grand Redesign

* Team rebels about the messy codebase, management feel the pinch of productivity decrease and agree to redesign
* Tiger team is formed. Everyone wants to be in tiger team -> green field project
* Two teams are in race. The new team should build everything and adds on which the old team does.
* Management does not replace the old system, unless the new system is completely ready.
* In some companies this race as gone for over 10 years quotes "Rober C Martin"

### Attitude

> What does good code rot to bad one?

Compains from developers
* Requirement changes which thwarts intial design
* Tight schedules
* We harp about bad managers, intolerant customer and poor marketing startegies

> * The fault is on us, bitter pill to swallow!!!

* Tech, project and product managers look up to us for information.
* Don't be shy in telling them what you think
* Most managers want the truth eventhough though they dont act like it. They want good code even when they are obsessing about schedules.
* They may defend the requirements and the schedule, it is our job to defend the code.


### The Art of Clean Code

* Programmers require "code-sense". A programmer with code sense can look at a messy code and see options and variations.
* Code sense helps programmers choose from the best of the variations and transform the code from messy to an elegant one.

### Boy Scout Rule

* Its not about writing clean code once, it is about continuing to maintain clean code.
American Boy Scout Rule
> Leave the campground cleaner than you found it.

## Meaningful Names

1. Use intention revealing names
2. Avoid Disinformation
    - Grouping of accounts as accountList instead of accountGroup
    - hp, aix, sco are unix variable names. These obsure the meanining of the variable
3. Make meaning distinctions - Do not add noise words or numbers just because the compiler demands it.
    - If names must be different, they should also mean something different.
4. Use pronouncable names
    - Eg.., of some poor variable names: genymdhms (generation date, yeat, month, day, hours etc..,)
    - Programming is a social activity ensure that the variable names are pronounable and colloboarated with.
5. Use searchable names
    - MAX_CLASSES_PER_STUDENT is easily greppable than a number 7.
6. Interfaces and Implementation
    - Leave interfaces unadored. eg.., IShapeFactory is unecessary.
    - Distraction and too much information
    - Add encoding to implementation if necessary.
7. Class Names should be Nouns and Method Names should be Verbs
8. Dont be cute - Will be memorable or connect with people who are inline with your humor.
    - Eg.., HolyHandGrenade - May be deleteItems is better.
9. Pick one word per concept
    - eg.., fetch, retrive, get
10. If it depends use solution domain names
    - Use computer algorithm names, pattern names, math names etc..,
    - Its not necessary to choose every name from the problem domain, which might make co-worker to go back and forth with the customer to understand the name.
    - AccountVisitor is an example, a class which embodies Vistor pattern.
11. Add meaningful context as needed.
    - Eg.., firstName, lastName, street, city etc.., implicity mean they belong to an address.
    - What if we saw that11. Add meaningful context as needed.
    -   - Eg.., firstName, lastName, street, city etc.., taken together mean they belong to an class called address.
    -       - If only a variable called state is present it is difficult to understand the context of this variable, adding a meaning context to it makes sense.
    -       - Eg.., addrFirstName, addrState.
12. Dont add gratatious context
    - If you have an application called ULS, it is unecessary to prefix classes with names UlsDataStore etc..,
    - Be helpful to your IDE so that searches with a letter U for eg.., dont result in a large result set.


## Fucntions

1. Functions should be small, but how small?
    - Depending on the context functions can range from 5 - 10 lines as per ULS guidelines
    - Each function should be transparently obvious
    - Each should tell a story
    - Each should lead to a compelling order
2. Do one thing
    - Functions should do one thing, they should do it well.They should do it only.
3. One level of abstraction per function
    - mixing very high level, intemediate and low level abstractions
    - x.getHtml() high level of abstraction, PageParse.parsePage() is intermediate, StringBuffer.append() is low level
    - All the above in a single method, just reduces the cognitive sense of the reader.
4. Step down rule
    - Code should be top-down narrative
    - Every function to be followed by those at the next level of abstraction, descend one level of abstraction at a time
    - Reading a program should be like a set of `TO paragraphs
    - To do x which requires Y, To perform Y etc..,
5. Switch S`tatements
    - switch statements always tend to do N things
    - Bury switch statements at a level so that they are not repeated anywhere
    - Employee eg: 

```
public Money calculatePay(Employee e) {
    switch(e.type()) {
        case COMMISIONED:
            return calculateCommisionpay(e);
        case SALAIRED:
            return calculateSalariedPay(e);
        default:
            throw new IllegalArgumentException("unknown");
    }
}

```
    - Violates SRP and OCP, more than one reason for change and changes whenever new types are added respectively.
    - Many underlying functions will start using the same structure, because we need to pass on the Employee(e) object.
    - Use an abstract factory instead

```
public class EmployeeFactoryImpl implements EmployeeFactory {
    switch(er.getType()) {
        case COMMISIONED:
            return new CommissionedEmployee(er);
        case SALARIED:
            return new SalariedEmployee(er);
        default:
            throw new InvalidEmployeeType("unknown");
    }
}

public abstract class Employee {
    public abstract boolean isPayDay();
    public abstrct Long calculatePay();
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord er) throws InvalidEmployeeType;
}


public static void main() {
    EmployeeRecord er = new EmployeeRecord("COMMISIONED");
    ComissionedEmployee ce = EmployeeFactory.makeEmployee(er);
    ce.isPayDay();
}
```
