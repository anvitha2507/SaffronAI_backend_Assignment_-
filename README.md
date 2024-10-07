# SaffronAI_backend_Assignment_-
**Portfolio Value, Gain, and XIRR Calculation**  
**Overview**  
This Python script calculates the total portfolio value, gain, and XIRR (Extended Internal Rate of Return) based on mutual fund transactions. It utilizes the **mstarpy** library to fetch the latest Net Asset Value (NAV) of mutual funds and applies a FIFO (First-In-First-Out) approach to manage holdings. The script processes a JSON file that contains mutual fund transaction data and provides key portfolio metrics such as:<br>

*Total Investment.  
*Current Portfolio Value.  
*Portfolio Gain.  
*XIRR (percentage return on investment).  


**Key Features**  
**NAV Retrieval:** The script dynamically fetches the current NAV for each mutual fund based on its ISIN using the mstarpy library, with caching to optimize performance.

**FIFO for Transactions:** The script uses a FIFO mechanism to accurately track the sale of mutual fund units, ensuring gains or losses are calculated based on the acquisition price of the oldest units first. 

**XIRR Calculation:** It computes the XIRR using the cash flows from the transactions, including both investments and redemptions, along with the current value of remaining holdings.  

**Error Handling:** In case the NAV retrieval fails or the XIRR calculation encounters issues, the script handles the errors gracefully and provides useful feedback.
Dependencies  

**Before running the script, you must install the following dependencies:**-
-Python 3.x  
-mstarpy for fetching mutual fund NAVs  
-Standard Python libraries:
-json  
-datetime  
-collections  
-deque  
-defaultdict  
-typing  


**To install the mstarpy library, use the following command:**

**pip install mstarpy**

**JSON Data Structure**
The input data is a JSON file that contains mutual fund transactions. The expected structure is as follows:


{  
  "data": [  
    {  
      "dtTransaction": [  
        {  
          "trxnUnits": "number of units",  
          "trxnAmount": "transaction amount",  
          "trxnDate": "transaction date (format: dd-MMM-yyyy)",  
          "isin": "fund's ISIN",  
          "folio": "folio number"  
        },  
        ...  
      ]  
    }  
  ]  
}  
Each transaction includes the number of units bought or sold, the transaction amount, the date of the transaction, and the ISIN of the mutual fund.

**How It Works**

**NAV Fetching:** For each transaction, the script uses the get_current_nav() function to fetch the latest NAV for the mutual fund. Results are cached to avoid redundant API calls.<br>

**Transaction Processing:** The transactions are processed one by one. For buy transactions, the script tracks the number of units and the acquisition price. For sell transactions, it applies the FIFO method to calculate the selling price and the gain/loss.

**Portfolio Metrics:** The script calculates the total investment, current portfolio value, and portfolio gain based on the processed transactions.

**XIRR Calculation:** The cash flows from the transactions (both investments and redemptions) are used to calculate the XIRR. The script uses an iterative method to compute the rate of return over the investment period.
