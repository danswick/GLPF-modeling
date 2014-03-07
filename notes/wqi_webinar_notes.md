#Water Quality tool for Indexing Agricultural Runoff Notes

###**Harbans Lal**, Environmental Engineer 
####*National Water Quality/Quantity Team, WNTSC/USDA-NRCS, Portland, OR*

- WQI: parameters expressed in different units and measured in different ranges. 
	- "hard to understand and follow by non-professionals" thus the concept of WQI is introduced 
- WQI is a dimensionless number that combines the values of multiple WQ factors such as DO, pH, BOD, COD, Ecoli, Temp, Nutrients (N&P), etc.into a single value by normalized subjective rating curves 
	- "introduction to water quality index" in *Water Efficiency* journal
- Why agriculture? Ag needs & pollutes water. NRCS needs more tools for evaluating effectiveness of conservation practices. 
	- Planning and assessment tools (CPPE)
	- Modeling (CEAP, RUSLE2, etc) 
	- Edge of Field (EoF) monitoring 
- Available tools are either too generic or too expensive 
- [WQIAG: Water Quality Index for Runoff Water From Agricultural](http://www.waterefficiency.net/WE/Editorial/WQIAG_Water_Quality_Index_for_Runoff_Water_From_Ag_19046.aspx)
- WQIAG is a live web tool. Requires Silverlight for some ungodly reason. 
	- Ranks runoff from ag fields (1-10): 10 being the best
	- Mult. field characteristics and mgmt factors
	- Weighting for different factors for local prefs
	- Site-specific weather data with the possibility (?) of customization
- Tool demo
	- Need HUC number? 
	- Application rate is as a % of LGU recommendations 

###**Brooks Engelhardt**, Resource Conservationist, USDA-NRCS
####*Use of the Runoff WQ Index in Ventura County, CA*

- EQIP case study. WQI in a citrus orchard. 
	- Lemon orchard treated with cover crop. 

###Concluding remarks
- WQIag incorps professional knowledge and local preferences through weighting factors
- Low cost, low (did he mean high?) rigor, high intensity usage tool for first level of approximation 
- Highly useful when actual monitoring is out of reach 

###Future Plans
- Re-designing nutrient management componenet and tile drain system 
- Extending WQIag framework at the hwole farm and watershed level
_ Working with the Idaho National Lab of the US-DOE to link with their LEAF framework for evaluating water quality at landscape level
- Calibration with actual monitoring and other models 
- Been in talks with discovery and pioneer farms for calibration 

###Q/A
- Is this a re-do of the NRCS water quality indicator of 20 years ago? 
- Field index only 
- What about PI? 
	- PI does not give you a ranking of water that might be exiting the field (?)
- Will this tool be incorporated into CDSI? 
	- Maybe, but it would be a long process. 
- How does this compare to [NTT](http://nn.tarleton.edu/NTTWebARS/)
	- He has been part of developing NTT, which is based on APEX and is quantitative. WQI is only a **ranking tool** and does not attempt to quantify. 
- How well does the tool respond to extreme weather? 
	- It doesn't. Monthly averages are the only option. 
- State-specific parameters? 
	- Use tool as it is. If weighting factors are not sufficient, contact your state office. 