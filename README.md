# Data-Modeling-Calculated-Columns-Created-Calculated-Columns-using-DAX
In this exercise I learnt how to create columns of different measures in POWER BI using DAX Formulas like calculate, var, relatable, max etc. 

1. **Creating Post Invoice Deduction**

  I need the Post Invoice Deduction amount appearing in the fact_actuals_estimate table as a new column which is the next time in our P & L.
  Steps I used creating post_invoice_deduction_amount:
  1. Firstly, I have two tables Fact_actuals_estimate and post_invoice_deductions and you are adding this “post_invoice_deduction_amount” column into the Fact_actuals_estimates.
  2. As the data model and the relationships are perfectly set up, so for each customer_code and for that product_code on that particular date you need to get the discount_pct and other_deduction_pct from the                    post_invoice_deduction table. I multiplied that with net_invoice_sales_amount to get post deduction amounts. It’s sort of performing a left outer join.
  3. Before that, I understood that the working of CALCULATE() function and how it achieving the desired functionality
     { CALCULATE(
                Column_name,                  //desired column want to add from another table
                RELATEDTABLE(table_name)      //formula to fetch the desired column from related table
     ) }
4. Now, I decided to decode the entire formula used for calculating “post_invoice_deduction_amount”
 {  post_invoice_deduction_amount =
          var res = CALCULATE(
                    MAX(                                      // Aggregate function
                    post_invoice_deductions[discounts_pct]),  // the column you need for P&L values “discount_pct”
                    RELATEDTABLE(post_invoice_deductions))    // the related table you want in which column resides
                    return res * fact_actuals_estimates[net_invoice_sales_amount] // getting the post invoice deduction amount by multiplying discount with net invoice sales.
 }
 
