#  Change length of character variable and remove formats and informats  
    Change length of character variable and remove formats and informats                                                                          
                                                                                                                                                  
    Interesting note                                                                                                                              
                                                                                                                                                  
      SAS documentation states that you can modify informat, format, and label with proc sql alter table modify.                                  
      However, you cannot remove formats or informats.                                                                                            
                                                                                                                                                  
      It is also interesting that you can make length changes but not remove formats or informats with sql alter.                                 
                                                                                                                                                  
    GitHub                                                                                                                                        
    https://cutt.ly/ogGkJEG                                                                                                                       
    https://github.com/rogerjdeangelis/https-communities.sas.com-t5-SAS-Programming-change-the-length-of-a-charachter-variable-proc-sql-m         
                                                                                                                                                  
    SAS Forum                                                                                                                                     
    https://cutt.ly/jgGpuRD                                                                                                                       
    https://communities.sas.com/t5/New-SAS-User/Change-length-of-character-variable-and-remove-format-and/m-p/696777                              
                                                                                                                                                  
    SAS Forum                                                                                                                                     
    https://cutt.ly/hgGkbks                                                                                                                       
    https://communities.sas.com/t5/SAS-Programming/change-the-length-of-a-charachter-variable-proc-sql-modify/td-p/279975                         
                                                                                                                                                  
    *                                                                                                                                             
    #####  #   #  ####   #   #  #####                                                                                                             
      #    ##  #  #   #  #   #    #                                                                                                               
      #    # # #  #   #  #   #    #                                                                                                               
      #    #  ##  ####   #   #    #                                                                                                               
      #    #   #  #      #   #    #                                                                                                               
      #    #   #  #      #   #    #                                                                                                               
    #####  #   #  #       ###     #                                                                                                               
    ;                                                                                                                                             
                                                                                                                                                  
    data have;                                                                                                                                    
      attrib SSN length=$12 format=$12. informat=$12. ;                                                                                           
      input ssn;                                                                                                                                  
    cards4;                                                                                                                                       
    485-40-2594                                                                                                                                   
    ;;;;                                                                                                                                          
    run;quit;                                                                                                                                     
                                                                                                                                                  
    #    Variable    Type    Len    Format    Informat                                                                                            
                                                                                                                                                  
    1    SSN         Char     20    $12.      $12.                                                                                                
    *                                                                                                                                             
     ###   #   #  #####  ####   #   #  #####                                                                                                      
    #   #  #   #    #    #   #  #   #    #                                                                                                        
    #   #  #   #    #    #   #  #   #    #                                                                                                        
    #   #  #   #    #    ####   #   #    #                                                                                                        
    #   #  #   #    #    #      #   #    #                                                                                                        
    #   #  #   #    #    #      #   #    #                                                                                                        
     ###    ###     #    #       ###     #                                                                                                        
    ;                                                                                                                                             
                                                                                                                                                  
    #    Variable    Type    Len                                                                                                                  
                                                                                                                                                  
    1    SSN         Char     40   ==> lrngth doubled - no formats or informats;                                                                  
                                                                                                                                                  
    *                                                                                                                                             
    ####   ####    ###    ###   #####   ###    ###                                                                                                
    #   #  #   #  #   #  #   #  #      #   #  #   #                                                                                               
    #   #  #   #  #   #  #      #       #      #                                                                                                  
    ####   ####   #   #  #      ####     #      #                                                                                                 
    #      # #    #   #  #      #         #      #                                                                                                
    #      #  #   #   #  #   #  #      #   #  #   #                                                                                               
    #      #   #   ###    ###   #####   ###    ###                                                                                                
    ;                                                                                                                                             
                                                                                                                                                  
    data have;                                                                                                                                    
      attrib SSN length=$12 format=$12. informat=$12. label="Social Security Number" ;                                                            
      input ssn;                                                                                                                                  
    cards4;                                                                                                                                       
    485-40-2594                                                                                                                                   
    ;;;;                                                                                                                                          
    run;quit;                                                                                                                                     
                                                                                                                                                  
    proc sql;                                                                                                                                     
       alter table have                                                                                                                           
          modify ssn char(40) ;                                                                                                                   
    ;quit;                                                                                                                                        
                                                                                                                                                  
    proc datasets lib=work;                                                                                                                       
        modify have;                                                                                                                              
         attrib _all_ label=' ';                                                                                                                  
         attrib _all_ format=;                                                                                                                    
         attrib _all_ informat=;                                                                                                                  
         contents data=have;                                                                                                                      
    run;quit;                                                                                                                                     
                                                                                                                                                  
    BEFORE                                                                                                                                        
    ======                                                                                                                                        
                                                                                                                                                  
    #    Variable    Type    Len    Format    Informat                                                                                            
                                                                                                                                                  
    1    SSN         Char     20    $12.      $12.                                                                                                
                                                                                                                                                  
    AFTER                                                                                                                                         
    =====                                                                                                                                         
                                                                                                                                                  
    #    Variable    Type    Len                                                                                                                  
                                                                                                                                                  
    1    SSN         Char     40                                                                                                                  
                                                                                                                                                  
                                                                                                                                                  
