# utl-grubs-test-for-outliers-using-r-package-outliers
Outlier package has a half dozen algorithms for outlier analysis.
    Grubs test for outliers using r package outliers                                                  
                                                                                                      
    Outlier package has a half dozen algorithms for outlier analysis                                  
                                                                                                      
    TWO TESTS                                                                                         
    =========                                                                                         
                                                                                                      
      TYPE   = 10 -- test for one outlier                                                             
             = 11 -- test for small and large outlier                                                 
                                                                                                      
    INPUT                                                                                             
    =====                                                                                             
                                                                                                      
    WORK.SHOES total obs=395                                                                          
                                                                                                      
     REGION    PRODUCT           SUBSIDIARY      SALES                                                
                                                                                                      
     Africa    Boot              Addis Ababa     29761                                                
     Africa    Men's Casual      Addis Ababa     67242                                                
     Africa    Men's Dress       Addis Ababa     76793                                                
     Africa    Sandal            Addis Ababa     62819                                                
     Africa    Slipper           Addis Ababa     68641                                                
     Africa    Sport Shoe        Addis Ababa      1690                                                
     Africa    Women's Casual    Addis Ababa     51541                                                
     Africa    Women's Dress     Addis Ababa    108942                                                
                                                                                                      
                                                                                                      
    EXAMPLE OUTPUT                                                                                    
    --------------                                                                                    
                                                                                                      
     TYPE=10  (one outlier)                                                                           
     ----------------------                                                                           
                                                                                                      
      Grubbs test for one outlier                                                                     
                                                                                                      
      data:  have$SALES                                                                               
                                                                                                      
      G = 9.39540, U = 0.77539, p-value < 2.2e-16                                                     
      alternative hypothesis: highest value 1298717 is an outlier                                     
                                                                                                      
      %put &=outlier                                                                                  
                                                                                                      
      817   %put &=outlier;                                                                           
      OUTLIER=highest value 1298717 is an outlier                                                     
                                                                                                      
                                                                                                      
     TYPE=11  (low and high outliers)                                                                 
     ---------------------------------                                                                
                                                                                                      
      Grubbs test for two opposite outliers                                                           
                                                                                                      
      data:  have$SALES                                                                               
                                                                                                      
      G = 10.05700, U = 0.77435, p-value < 2.2e-16                                                    
      alternative hypothesis: 325 and 1298717 are outliers                                            
                                                                                                      
      %put &=outlier;                                                                                 
                                                                                                      
      OUTLIER=325 and 1298717 are outliers                                                            
                                                                                                      
                                                                                                      
    PROCESS (R WORKING CODE)                                                                          
    =========================                                                                         
                                                                                                      
      TYPE=10                                                                                         
      --------                                                                                        
                                                                                                      
         res<-grubbs.test(have$SALES, type = 10);                                                     
                                                                                                      
                                                                                                      
      TYPE=20                                                                                         
      --------                                                                                        
                                                                                                      
         res<-grubbs.test(have$SALES, type = 10);                                                     
                                                                                                      
    OUTPUT                                                                                            
    ======                                                                                            
                                                                                                      
     SEE ABOVE                                                                                        
                                                                                                      
                                                                                                      
     *                _              _       _                                                        
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _                                                  
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |                                                 
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |                                                 
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|                                                 
                                                                                                      
    ;                                                                                                 
                                                                                                      
    options validvarname=upcase;                                                                      
    libname sd1 "d:/sd1";                                                                             
    data sd1.have;                                                                                    
      set sashelp.shoes(keep=region product subsidiary sales);                                        
    run;quit;                                                                                         
                                                                                                      
    *          _       _   _                                                                          
     ___  ___ | |_   _| |_(_) ___  _ __                                                               
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                              
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                             
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                             
                                                                                                      
    ;                                                                                                 
                                                                                                      
                                                                                                      
    TYPE=10                                                                                           
    --------                                                                                          
                                                                                                      
    %utl_submit_r64("                                                                                 
    library(haven);                                                                                   
    library(outliers);                                                                                
    library(SASxport);                                                                                
    have<-read_sas('d:/sd1/have.sas7bdat');                                                           
    head(have);                                                                                       
    res<-grubbs.test(have$SALES, type = 10);                                                          
    res;                                                                                              
    writeClipboard(res$alternative);                                                                  
    ",returnVar=outlier  );                                                                           
                                                                                                      
    %put &=outlier;                                                                                   
                                                                                                      
                                                                                                      
    TYPE=10                                                                                           
    --------                                                                                          
                                                                                                      
    %utl_submit_r64("                                                                                 
    library(haven);                                                                                   
    library(outliers);                                                                                
    library(SASxport);                                                                                
    have<-read_sas('d:/sd1/have.sas7bdat');                                                           
    head(have);                                                                                       
    res<-grubbs.test(have$SALES, type = 11);                                                          
    res;                                                                                              
    writeClipboard(res$alternative);                                                                  
    ",returnVar=outlier  );                                                                           
                                                                                                      
    %put &=outlier;                                                                                   
                                                                                                      
