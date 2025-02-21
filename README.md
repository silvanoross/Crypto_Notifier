# Crypto_notifier

[Planning doc](https://docs.google.com/document/d/1rUZfldYmy9Eqa9YMD0Sh2NcjxjiFe94NhCzngBFl1-c/edit)

[Google Slides Presentation](https://docs.google.com/presentation/d/1Q2ZRGA01SbQB4v1tawb9DYXGLw8sZ-zitMHMYtC8o_U/edit#slide=id.g15b07a4b0c1_0_0)

The goal of this application is to deliver a comparison for user-chosen cryptocurrencies through a text message using the Twilio software package. The comparison is taking the historical return values of the currencies chosen and creating a threshold value which is used to compare daily return values of recent times. 


---

## Required Installs

### Language: Python 3.9.12

### Libraries used:

[Pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) - For the creation and manipulation of Data Frames

[Jupyter Labs](https://jupyter.org/) - An ipython kernel for interactive computing in python

[OS](https://docs.python.org/3/library/os.html) - Miscellaneous operating system interface

[Dotenv](https://github.com/motdotla/dotenv) - Module to load environment variables 

[Questionary](https://pypi.org/project/questionary/) - Python module for easy CLI interaction

[Coin Gecko API](https://www.coingecko.com/en/api/documentation) - A free comprehensive cryptocurrency API

[Twilio](https://www.twilio.com/docs/usage/api) - API for sending SMS to a phone number after setting up an account

---

## Installation Guide

This application has quite a few working parts and it is necessary to ensure that all the correct packages have been installed correctly.

Firstly, we recommend using setting up an Anaconda environment to run this application. Additionally, all commands are going to be assuming GitBash is being used as the terminal and conda has been intialized. You can download Anaconda and Git Bash here: [anaconda_link](https://www.anaconda.com/), [git_bash](https://git-scm.com/downloads)

To create the right conda environment through Git Bash enter

```python
    conda create -n myenv python=3.9
    conda activate myenv
```

First check that all of the anaconda associated packages have been installed by running:

```python
    conda list jupyter
    conda list pandas
```

Next the packages not included need to be installed and this can be accomplished by entering the following in the Git Bash terminal.

```python
    pip install questionary
    pip install python-dotenv
    pip install -U pycoingecko
    pip install twilio
```

To check that all of the dependencies have been installed by entering the following into the Git Bash Terminal:

```python
    conda list questionary
    conda list dotenv
    conda list pycoingecko
    conda list twilio
```

With all of these packages the conda environment should be set up to run the Crypto Notifier application

---

## Usage

Prior to running the application it is necessary to create a Twilio Account. Sign up at [https://www.twilio.com/](https://www.twilio.com/)

There are 3 important pieces of information that need to be retrieved: the Twilio phone number associated with your account, the Twilio account ID and the Twilio authentication token.

You can find this informatin on the main console page of your twilio account:

![twilio](images/twilio_info.png)

These peices of information need to be stored in a **.env** file that is saved in the same repo as this application. The information needs to look like the following:
> "TWILIO_ACCOUNT_ID" = 'YOUR ACCOUNT ID HERE'

> "TWILIO_AUTH_TOKEN" = 'YOUR AUTHENTICATION TOKEN HERE'

> "TWILIO_PHONE_NUMBER" = 'YOUR TWILIO PHONE NUMBER HERE'

Once the **.env** file has been created with an active Twilio phone number and credentials everything should be set up to run the application.

To run the application first activate the conda environment associated with the necessary packages and libraries. Navigate to this application's folder repo and run the application with the following commands:

```python
    conda activate myenv
    cd Crypto_notifer
    code .
```

It is advised to run this application in VS Code or another IDE as running it through the command line has shown to give issues with recognizing the environment variables.

One the program is running:

This will prompt the user to enter their 10 digit phone number:

![prompt](images/initial_prompt.png)

After entering a phone number the user will be given a choice of 5 crypto currencies to choose from 

![choices](images/crypto_options.png)

To select multiple cryptocurrencies for analysis the user must use the SPACE bar to highlight multiple currencies then press ENTER to advance through the program.

The final display will show:

![message_sent](images/message_sent.png)

You should receive a text message like the following:

![text_message](images/text_message.png)

---

## Highlights:

### Data Analysis

First we called the data for each individual cyrptocurrency: below is an example for one symbol.

![ripple](images/ripple_analysis.png)

Next we gathered the pct change and then took the absolute value to reflect the magnitude of the change:

![ripple_mag](images/ripple_pct_change.png)

Then we calculated the mean of pct change over the entire 18 months.  This is the threshold for each coin.

![ripple_threshold](images/ripple_threshold.png)

Finally we put all of the values in a combined dataframe for referencing during our comparisons:

![final](images/final_data_threshold.png)

The final thing we had to do was create a concatenated dataframe with two weeks of the most recent cryptocurrency data for the list given to the user. Then we had to compare each day's price against the threshold that we made. This looks like the following:

![2_week](images/2_week_pct_change.png)

This was a complicated conditional logic feat which was accomplished by looping through the symbols in the list. then looping through each day in the two week percent change data frame indexed on the symbol. Then comparing the two and pulling the symbols date and value into a list of messages to be sent to the user using twilio. This is displayed as the following: 

![conditional](images/conditional_logic.png)


---

## Contributors

Created by Ben Spiegel, Silvano Ross and Tracie Stipp while in the UW FinTech Bootcamp
> Contact Info:
>
> email: brspiegel@gmail.com |
> [GitHub](https://github.com/brspiegel) |
> [LinkedIn](https://www.linkedin.com/in/ben-spiegel-36753476/)
>
> email: stipptracie@gmail.com |
> [GitHub](https://github.com/stipptracie) |
> [LinkedIn](https://www.linkedin.com/in/tracie-stipp-0719691b/)
>
> email: silvanoross3@gmail.com |
> [GitHub](https://github.com/silvanoross) |
> [LinkedIn](https://www.linkedin.com/in/silvano-ross-b6a15a93/)

---

