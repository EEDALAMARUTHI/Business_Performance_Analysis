**Dax Queries**

**Finance View**
- Net sales =SUM(fact_actuals_estimates[net_sales_amount])
- Net sale Last year =CALCULATE(Key_Measure[NS $],SAMEPERIODLASTYEAR(dim_date[date]))
- Gross Margin =[NS $]-[Total_cogs $]
- Gross sales =SUM(fact_actuals_estimates[gross_sales_amount])
- GM % $ = DIVIDE([GM $],[NS $],0)
- GM % LY = CALCULATE(Key_Measure[GM % $],SAMEPERIODLASTYEAR(dim_date[date]))
- Net Profit % = DIVIDE([Net Profit],[NS $],0)
- Net Profit % LY = CALCULATE(Key_Measure[Net Profit %],SAMEPERIODLASTYEAR(dim_date[date]))
- Profit & Loss YoY Chg = [P & L Values]-[P & L LY]
- P & L YoY Chg % = DIVIDE(Key_Measure[P & L YoY Chg],[P & L LY],0)*100
- P & L LY = CALCULATE([P & L Values],SAMEPERIODLASTYEAR(dim_date[date])) 


**Supply Chain**
- Forecast Qty = 
var lsalesdate = MAX(fact_sales_monthly[date])
RETURN
CALCULATE(SUM(fact_forecast_monthly[forecast_quantity]),fact_forecast_monthly[date]<=lsalesdate)
- Forecast accuracy % = IF('Key_Measure'[ABS error %]<> Blank(),1- 'Key_Measure'[ABS error %],BLANK())
- Net error = [Forecast Qty]-Key_Measure[sales Qty]
- Net Error LY = CALCULATE(Key_Measure[Net error],SAMEPERIODLASTYEAR(dim_date[date]))
- Net Error % = DIVIDE([Net error],[Forecast Qty],0)*100
- ABS error = 
SUMX(DISTINCT(dim_date[date]),
SUMX(DISTINCT(dim_product[product_code]),ABS([Net error])))
- ABS error Ly = CALCULATE([ABS error],SAMEPERIODLASTYEAR(dim_date[date]))
- ABS error % = DIVIDE([ABS error],[Forecast Qty],0)


**Sales View**
- Total_cogs $ = [MC $]+[FCA $]+[FCoA $]
  
  **Other Dax Quries**
  - ads & Promotions = SUM(fact_actuals_estimates[ads_promotions])
  - Benchmark_value = [NIS $]-[NIS India $]
  - FCA $ = SUM(fact_actuals_estimates[freight_cost])
  - FCoA $ = SUM(fact_actuals_estimates[freight_other_amount])
  - GM/Unit = DIVIDE([GM $],[Quantity],0)
  - Market share % = DIVIDE(SUM('Market share'[Sales $]),SUM('Market share'[total_market_sales_$]),0)
  - Operational expenses $ = (Key_Measure[ads & Promotions]+[Other_promotions])*-1
  - Other_promotions = SUM(fact_actuals_estimates[other_promotions])
  - Performance Visual title = Key_Measure[selected P & L rows] & " Performance over time"
  - PID $ = [Gs $]-[NIS $]
  - PIDisc $ = SUM(fact_actuals_estimates[post_invoice_deductions_amount])
  - PIDO $ = SUM(fact_actuals_estimates[post_invoice_other_deductions_amount])
  - Quantity = SUM(fact_actuals_estimates[Qty])
  - Risk = IF([Net error]>0, "Excesss inventory", IF([Net error]<0, "out of stock", BLANK()))
  - Top/Bottom N title = "Top/bottom Products & Customers by " & 'Key_Measure'[selected P & L rows]
  - Total PIDisc $ = [PIDisc $]+[PIDO $]

**Key Insights**
Big Sales Jump, But Profit Plummeted: Sales soared by 170.65% to $136.04 million, but net profit crashed by 37.64% to -$2.28 million. This means the company sold a lot more, but lost money overall.
Costs Exploded: Major cost increases ate into profits:
Manufacturing costs nearly doubled (+99.01%).
Freight costs more than doubled (+138.22%).
Operational expenses also rose sharply (+105.64%).
Gross Margin Improvement Didn't Help: While the gross margin percentage improved slightly (from 31.04% to 32.54%), the massive increase in the cost of goods sold meant that this small percentage gain was not enough to offset the huge increase in expenses.
Excess Inventory is a Problem: The company has too much inventory, which is a sign of poor planning or forecasting. This ties up cash and could lead to losses if the inventory becomes obsolete.
Regional Sales Skewed: Most sales came from the Asia-Pacific (APAC) region.
Missing Details: The provided information lacks detail about which products or customers are driving the sales growth and which are contributing to the losses. This makes it hard to pinpoint the exact problems.













