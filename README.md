
# Pytest CodeAlong

## Introduction

In this lesson, we'll see some examples of unit tests with the most popular testing framework in Python, Pytest! 

In the last lesson, we learned a bit about **_Unit Tests_** and how they allow us to write code using the **_Test-Driven Development (TDD)_** methodology, including why it is important to programmers everywhere and how it protects us from accidentally breaking everything anytime we add new code. In this lesson, we'll see some examples of unit tests, and write some corresponding code to make them pass. 


## Scripts vs Jupyter Notebooks

**_NOTE:_** Before we begin, it's worth noting that most testing is done through the use of a scripting with Python, rather than live in a Jupyter notebook. In the real world, developers would typically write all their tests in a file starting with `test_`, and then run that test using the Pytest Framework directly in a terminal window. However, it is possible to run Pytest in a jupyter notebook directly by making use of some specialized libraries for this specific purpose. Since our goal for this lab is to just get a better grasp on testing and see what basic tests and the "Red-Green-Refactor" workflow looks like, we'll save ourselves the additional complexity of creating a script and running it locally and just run our tests directly in this notebook. Just be aware that when you see these tests in the real world (or when you need to write some yourself), they'll likely be in scripts, not jupyter notebooks.

## Getting Started

In order to run this notebook, we'll need to quickly ensure that we have two important libraries installed: **_Pytest_**, the testing framework we'll use to run our tests, and **_ipytest_**, a small library written to allow people to run their tests directly inside a jupyter notebook. 

Run the two following cells to ensure that you have both libraries.


```python
!pip install pytest
```

    Requirement already satisfied: pytest in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (4.0.0)
    Requirement already satisfied: py>=1.5.0 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (1.7.0)
    Requirement already satisfied: six>=1.10.0 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (1.11.0)
    Requirement already satisfied: setuptools in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (40.6.2)
    Requirement already satisfied: attrs>=17.4.0 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (18.2.0)
    Requirement already satisfied: more-itertools>=4.0.0 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (4.3.0)
    Requirement already satisfied: atomicwrites>=1.0 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (1.2.1)
    Requirement already satisfied: pluggy>=0.7 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (0.8.0)
    Requirement already satisfied: colorama in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from pytest) (0.4.0)
    


```python
!pip install ipytest
```

    Collecting ipytest
      Downloading https://files.pythonhosted.org/packages/8d/3e/95fac18d9e4df6dcad1f1a8a12e8af6ad7e634845f852545b85fa0019e9a/ipytest-0.7.1-py3-none-any.whl
    Requirement already satisfied: packaging in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from ipytest) (18.0)
    Requirement already satisfied: pyparsing>=2.0.2 in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from packaging->ipytest) (2.3.0)
    Requirement already satisfied: six in c:\users\medio\appdata\local\continuum\anaconda3\lib\site-packages (from packaging->ipytest) (1.11.0)
    Installing collected packages: ipytest
    Successfully installed ipytest-0.7.1
    

### Some ipytest Boilerplate

The following code is boilerplate required to run Pytest inside a jupyter notebook. This is not code that would be included when writing tests in a real world environment. For more information on the library we're using to run pytest inside this jupyter notebook, check out the [ipytest documentation](https://github.com/chmp/ipytest).


```python
import ipytest
ipytest.config(rewrite_asserts=True, magics=True)

__file__ = "index.ipynb"
```

## Using Red-Green-Refactor to Write Tests

### Step 1: Red

Now, in the cell below, we'll write our first test. For this function, we'll write a test to check a function that adds two numbers together. While this is a pretty simple example, the methodology holds true. We start by picking a test case. Checking that 4 + 3 outputs 7 is as good as any example, so let's start there. 

We'll also declare the function that we are going to test, but we'll leave the body of the function empty. Remember, we start by writing a test that will fail by default, because the function that we're testing won't have been implemented yet. Instead, we focus on the output we expect the function should give us when we give it a certain input. Once we know that, we can easily create the body of the test by following a simple pattern:

1. Define the answer that you expect the function should give you for the inputs you've chosen. 
2. Call the function and pass in the inputs you selected. Store the output in a variable. 
3. Compare the function's output with the expected answer we stored using the `assert` keyword, so that the function will throw an error if the two don't match up. 



```python
def add_two_numbers(num_1, num_2):
    pass

def test_add_two_numbers():
    answer = 4 + 3                                 # Step 1
    func_output = add_two_numbers(4, 3)            # Step 2
    assert answer == func_output                   # Step 3
```

Now that we have our test, all that we have to do is run pytest! Pytest will automatically run any function that starts with `test_`, so it'll grab our `test_add_two_numbers` function and run it. We expect this test to fail, because we haven't finished `add_two_numbers` yet. This means that step 2 will store `None` instead of 7, which means that our assert statement will fail because `7` does not equal `None`. Let's run the cell below and examine the output we get. 


```python
ipytest.run()
```

    ============================= test session starts =============================
    platform win32 -- Python 3.6.7, pytest-4.0.0, py-1.7.0, pluggy-0.8.0
    rootdir: C:\Users\medio\Desktop\chevron-tdd\dsc-enterprise-pytest-codealong, inifile:
    plugins: remotedata-0.3.1, openfiles-0.3.0, faulthandler-1.5.0, doctestplus-0.2.0, arraydiff-0.2
    collected 1 item
    
    index.py F                                                               [100%]
    
    ================================== FAILURES ===================================
    ____________________________ test_add_two_numbers _____________________________
    
        def test_add_two_numbers():
            answer = 4 + 3
            func_output = add_two_numbers(4, 3)
    >       assert answer == func_output
    E       assert 7 == None
    
    <ipython-input-10-5330014502fb>:7: AssertionError
    ============================== warnings summary ===============================
    C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_remotedata
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_openfiles
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_faulthandler
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_doctestplus
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_arraydiff
        self.config,
    
    -- Docs: https://docs.pytest.org/en/latest/warnings.html
    ==================== 1 failed, 5 warnings in 0.14 seconds =====================
    

## Interpreting the Output

Pytest is an awesome testing framework because it makes it really easy to see what tests have failed, and it even shows you the line that's causing the problem in each function! In this one, we can see our assert statement is throwing an error, as we expected. It even shows us the value for each of the variables in the assert statement, so that we can clearly see it as the computer saw it when running the test!

**_NOTE:_** If pytest also returned some warnings, don't worry about them. These are warnings triggered by loading the library that runs pytest for us. You can safely ignore them in this case, and shouldn't expect to see anything like this when running real test scripts in a terminal. 

## Step 2: Green

Now that we have a working (failing) test like we needed, we'll continue on to step 2 and finish our `add_two_numbers` function. If we complete this function correctly, then when we rerun our test, this time everything should pass! Run the cell below to update the `add_two_numbers` function. 


```python
def add_two_numbers(num_1, num_2):
    answer = num_1 + num_2
    return answer
```

Now, let's rerun pytest and see how our output changes. 


```python
ipytest.run()
```

    ============================= test session starts =============================
    platform win32 -- Python 3.6.7, pytest-4.0.0, py-1.7.0, pluggy-0.8.0
    rootdir: C:\Users\medio\Desktop\chevron-tdd\dsc-enterprise-pytest-codealong, inifile:
    plugins: remotedata-0.3.1, openfiles-0.3.0, faulthandler-1.5.0, doctestplus-0.2.0, arraydiff-0.2
    collected 1 item
    
    index.py .                                                               [100%]
    
    ============================== warnings summary ===============================
    C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_remotedata
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_openfiles
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_faulthandler
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_doctestplus
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_arraydiff
        self.config,
    
    -- Docs: https://docs.pytest.org/en/latest/warnings.html
    ==================== 1 passed, 5 warnings in 0.04 seconds =====================
    

This time, everything passes! Awesome. 

## Step 3: Refactor

Once we have some basic working code, the final step is improve that code. This is where we would clean up our code, and try to implement better solutions. Note that we purposefully don't do that when trying to write a passing test in step 2. During step 2, our goal is to get across the finish line as quickly as possible. We're trying to write code that makes the test pass, but we still consider it a "rough draft", and assume that we'll be making updates and improvements later. This way, we always have a basic solution, and we'll be able know for sure that our refactored code actually works the way it's supposed to. Refactored code is usually more concise, more modular, and often optimized to be faster. Unfortunately, better solutions are always harder to arrive at than easier solutions, so we'll want to make sure our cleverness during the refactor doesn't turn around and bite us by introducing some other mistakes or breaking some existing functionality elsewhere in the system. 

Run the cell below to refactor our example `add_two_numbers` function. 


```python
def add_two_numbers(num_1, num_2):
    return num_1 + num_2
```

Now, run the cell below to rerun our test function with pytest and ensure that our refactored code didn't break anything. 


```python
ipytest.run()
```

    ============================= test session starts =============================
    platform win32 -- Python 3.6.7, pytest-4.0.0, py-1.7.0, pluggy-0.8.0
    rootdir: C:\Users\medio\Desktop\chevron-tdd\dsc-enterprise-pytest-codealong, inifile:
    plugins: remotedata-0.3.1, openfiles-0.3.0, faulthandler-1.5.0, doctestplus-0.2.0, arraydiff-0.2
    collected 1 item
    
    index.py .                                                               [100%]
    
    ============================== warnings summary ===============================
    C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_remotedata
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_openfiles
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_faulthandler
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_doctestplus
        self.config,
      C:\Users\medio\AppData\Local\Continuum\anaconda3\lib\site-packages\_pytest\assertion\rewrite.py:272: PytestWarning: Module already imported so cannot be rewritten: pytest_arraydiff
        self.config,
    
    -- Docs: https://docs.pytest.org/en/latest/warnings.html
    ==================== 1 passed, 5 warnings in 0.04 seconds =====================
    

It works! Our test didn't fail, which means that our refactoring of the code didn't break anything. 

## Testing in a Real-World Environment

When working with a toy example like this one, it can sometimes be hard to see the benefit that comes from writing all the extra code for testing. However, it makes more sense when you consider what a real-world test suite looks like. Imagine that you're new to the team, and you're asked to clean up some old code that could be done in a faster or cheaper way. How do you that other systems you aren't even aware of don't rely on the code you're changing? What if the changes you make to that code break a bunch of things that you aren't aware of? If a team has good **_test coverage_**, then they'll have a large suite of tests that confirm each major piece of functionality at every level of the their codebase. This way, if the code that you write breaks some code that relied on some code that relied on some other code that used the code you just changed, you'll still know about it, and will be able to make sure you correct the problem. When working with your own code on smaller scale projects, testing may seem tedious, but when working on massive, million-line codebases, they become your lifeline to make sure that you can confidently do work and change code around without worrying about breaking everything and losing your job. 

## Summary

In this lesson, we used the **_Red Green Refactor_** pattern with a toy example to create a failing test, write the function that makes the test work, and then used that test to ensure that changes that we made to the code gave the same output and kept the same overall functionality of the function before our changes. 
