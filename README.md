# CombineLimitSetting


Go to 
 /user/ivanpari/CombineLimitSetting/CMSSW_7_4_7/src/HiggsAnalysis/CombinedLimit
 
 combine cards
 combineCards.py datacards/Zut_singletop_uuu_BRtest.txt datacards/Zut_singletop_uuu_SR.txt > Zut_singletop_uuu.txt

 
 
 Run combine tool 
 combine -M Asymptotic datacards/uuu.txt -N nameoutputfile



Make a workspace of your datacard: (is safer than .txt )
 > text2workspace.py datacard.txt -m 125 -o datacard.root
 


Get an idea of the signal strength vales we need to build test-stat distrubutions: 
 > combine -M Asymptotic datacard.root   --> Gives r values: get uppper and lowerbound  for a range of r
 
Use Hybrid New method: 
  > combineTool.py -M HybridNew -d datacard.root --testStat LHC --freq --singlePoint rmin:rmax:stepsize -T 2000 -s -1 --saveToys --saveHybridResult 
  
  ignore: [#0] WARNING:Eval -- RooStatsUtils::MakeNuisancePdf - no constraints found on nuisance parameters in the input model
  
Get Nuissance parameter impacts: 
   Fit for each POI 
   > combineTool.py -M Impacts -d datacard.root -m 125 --doInitialFit --robustFit 1
  
  Scan each nuissance parameter
   > combineTool.py -M Impacts -d datacard.root -m 125 --robustFit 1 --doFits --parallel x
   
   Combine output into a JSON file
   > combineTool.py -M Impacts -d datacard.root -m 125 -o impacts.json
  
  Plot summarising the nuissance parameter pulls and impacts
   > plotImpacts.py -i impacts.json -o impacts
   
   
   
 
 
