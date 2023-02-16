
1. Java exceptions are designed to help you write code that covers all possible execution paths. 
This includes normal operations, exceptional situations, and unknown exceptional situations. 
This is shown below:

```
try{    
    // code for normal course of action
} catch(SecurityException se) {
    // code for known exceptional situation
    System.out.println("No permission!");
}
catch(Throwable t) {
    // code for unknown exceptional situations
    System.out.println("Some problem in copying: "+t.getMessage());
    t.printStackTrace();
}
```
