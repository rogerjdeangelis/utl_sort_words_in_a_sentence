# utl_sort_words_in_a_sentence
Sort words in a sentence (not so easy in SAS?)

    ```  Sort words in a sentence (not so easy in SAS?)                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  INPUT                                                                                                                                                        ```
    ```  =====                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```   SD1.HAVE total obs=4                       |   RULES (sort the words)                                                                                       ```
    ```                                             |                                                                                                                 ```
    ```     SENTENCE                                |   ALPHABETICAL                                                                                                  ```
    ```                                             |                                                                                                                 ```
    ```     some french women grow hairy orange     |   french grow hairy orange some women                                                                           ```
    ```     dogs can be affectionate                |   affectionate be can dogs                                                                                      ```
    ```     this house is blue                      |   blue house is this                                                                                            ```
    ```     select from where having orange         |   from having orange select where                                                                               ```
    ```                                                                                                                                                               ```
    ```  WORKING CODE (clean R code - not Klingon)                                                                                                                    ```
    ```  =========================================                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```     have$ALPHABETICAL <- sapply(strsplit(have$SENTENCE," "),function(x) paste(sort(x),collapse=" "));                                                         ```
    ```                                                                                                                                                               ```
    ```     data want;                                                                                                                                                ```
    ```       %utl_rens(xpt.have);                                                                                                                                    ```
    ```       set have;            * Note the long variable name 'ALPHABETICAL'                                                                                       ```
    ```                                                                                                                                                               ```
    ```  OUTPUT                                                                                                                                                       ```
    ```  ======                                                                                                                                                       ```
    ```     WORK.WANT total obs=4                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      SENTENCE                               ALPHABETICAL                                                                                                      ```
    ```                                                                                                                                                               ```
    ```      some french women grow hairy orange    french grow hairy orange some women                                                                               ```
    ```      dogs can be affectionate               affectionate be can dogs                                                                                          ```
    ```      this house is blue                     blue house is this                                                                                                ```
    ```      select from where having orange        from having orange select where                                                                                   ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/twwZga                                                                                                                                        ```
    ```  https://stackoverflow.com/questions/47304462/how-to-change-the-order-of-words-with-alphabetic-order                                                          ```
    ```                                                                                                                                                               ```
    ```  Moody Mudskipper profile                                                                                                                                     ```
    ```  https://stackoverflow.com/users/2270475/moody-mudskipper                                                                                                     ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  options validvarname=upcase;                                                                                                                                 ```
    ```  data sd1.have;                                                                                                                                               ```
    ```  length sentence $50;                                                                                                                                         ```
    ```  input;                                                                                                                                                       ```
    ```  sentence=_infile_;                                                                                                                                           ```
    ```  cards4;                                                                                                                                                      ```
    ```  some french women grow hairy orange                                                                                                                          ```
    ```  dogs can be affectionate                                                                                                                                     ```
    ```  this house is blue                                                                                                                                           ```
    ```  select from where having orange                                                                                                                              ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %utl_submit_r64('                                                                                                                                            ```
    ```  library(plyr);                                                                                                                                               ```
    ```  library(haven);                                                                                                                                              ```
    ```  library(SASxport);                                                                                                                                           ```
    ```  library(Hmisc);                                                                                                                                              ```
    ```  have<-as.data.frame(read_sas("d:/sd1/have.sas7bdat"));                                                                                                       ```
    ```  have$ALPHABETICAL <- sapply(strsplit(have$SENTENCE," "),function(x) paste(sort(x),collapse=" "));                                                            ```
    ```  have <- rename(have, c("ALPHABETICAL" = "ALPHA"));                                                                                                           ```
    ```  label(have$ALPHA)<-"ALPHABETICAL";                                                                                                                           ```
    ```  label(have$SENTENCE)<-"SENTENCE";                                                                                                                            ```
    ```  write.xport(have,file="d:/xpt/have.xpt");                                                                                                                    ```
    ```  ');                                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  libname xpt xport  "d:/xpt/have.xpt";                                                                                                                        ```
    ```  data want;                                                                                                                                                   ```
    ```    %utl_rens(xpt.have);                                                                                                                                       ```
    ```    set have;                                                                                                                                                  ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *_                                                                                                                                                           ```
    ```  | | ___   __ _                                                                                                                                               ```
    ```  | |/ _ \ / _` |                                                                                                                                              ```
    ```  | | (_) | (_| |                                                                                                                                              ```
    ```  |_|\___/ \__, |                                                                                                                                              ```
    ```           |___/                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  > library(plyr);library(haven);library(SASxport);library(Hmisc);                                                                                             ```
    ```  have<-as.data.frame(read_sas("d:/sd1/have.sas7bdat"));                                                                                                       ```
    ```  have$ALPHABETICAL <- sapply(strsplit(have$SENTENCE,"                                                                                                         ```
    ```  "),function(x) paste(sort(x),collapse=" "));                                                                                                                 ```
    ```  have <- rename(have, c("ALPHABETICAL" = "ALPHA"));                                                                                                           ```
    ```  label(have$ALPHA)<-"ALPHABETICAL";                                                                                                                           ```
    ```  label(have$SENTENCE)<-"SENTENCE";                                                                                                                            ```
    ```  write.xport(have,file="d:/xpt/have.xpt");                                                                                                                    ```
    ```  >                                                                                                                                                            ```
    ```  NOTE: 4 lines were written to file PRINT.                                                                                                                    ```
    ```  Stderr output:                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  Attaching package: 'Hmisc'                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  The following objects are masked from 'package:plyr':                                                                                                        ```
    ```                                                                                                                                                               ```
    ```      is.discrete, summarize                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  The following objects are masked from 'package:base':                                                                                                        ```
    ```                                                                                                                                                               ```
    ```      format.pval, round.POSIXt, trunc.POSIXt, units                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  NOTE: 2 records were read from the infile RUT.                                                                                                               ```
    ```        The minimum record length was 2.                                                                                                                       ```
    ```        The maximum record length was 373.                                                                                                                     ```
    ```  NOTE: DATA statement used (Total process time):                                                                                                              ```
    ```        real time           1.61 seconds                                                                                                                       ```
    ```        cpu time            0.04 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: Fileref RUT has been deassigned.                                                                                                                       ```
    ```  NOTE: Fileref R_PGM has been deassigned.                                                                                                                     ```
    ```  625   libname xpt xport  "d:/xpt/have.xpt";                                                                                                                  ```
    ```  NOTE: Libref XPT was successfully assigned as follows:                                                                                                       ```
    ```        Engine:        XPORT                                                                                                                                   ```
    ```        Physical Name: d:\xpt\have.xpt                                                                                                                         ```
    ```  626   data want;                                                                                                                                             ```
    ```  627     %utl_rens(xpt.have);                                                                                                                                 ```
    ```               Directory                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  Libref         WORK                                                                                                                                          ```
    ```  Engine         V9                                                                                                                                            ```
    ```  Physical Name  d:\wrk\_TD6076_E6420_                                                                                                                         ```
    ```  Filename       d:\wrk\_TD6076_E6420_                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                Member     File                                                                                                                                ```
    ```  #  Name       Type       Size  Last Modified                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  1  FUNCS      DATA     262144  11/16/2017 19:43:09                                                                                                           ```
    ```     FUNCS      INDEX     65536  11/16/2017 19:43:09                                                                                                           ```
    ```  2  FUNCTIONS  DATA     262144  11/16/2017 19:43:09                                                                                                           ```
    ```     FUNCTIONS  INDEX     65536  11/16/2017 19:43:09                                                                                                           ```
    ```  3  HAVE       VIEW      66560  11/16/2017 21:34:21                                                                                                           ```
    ```  4  WANT       DATA     131072  11/16/2017 21:34:21                                                                                                           ```
    ```  5  __REN001   DATA     131072  11/16/2017 21:34:21                                                                                                           ```
    ```  6  __REN002   DATA     131072  11/16/2017 21:34:21                                                                                                           ```
    ```  NOTE: The file WORK.IRIS (memtype=(DATA VIEW)) was not found, but appears on a DELETE statement.                                                             ```
    ```  NOTE: Deleting WORK.__REN001 (memtype=DATA).                                                                                                                 ```
    ```  NOTE: Deleting WORK.__REN002 (memtype=DATA).                                                                                                                 ```
    ```  NOTE: PROCEDURE DATASETS used (Total process time):                                                                                                          ```
    ```        real time           0.01 seconds                                                                                                                       ```
    ```        cpu time            0.01 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: There were 1 observations read from the data set XPT.HAVE.                                                                                             ```
    ```  NOTE: The data set WORK.__REN001 has 1 observations and 2 variables.                                                                                         ```
    ```  NOTE: DATA statement used (Total process time):                                                                                                              ```
    ```        real time           0.00 seconds                                                                                                                       ```
    ```        cpu time            0.00 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: There were 1 observations read from the data set WORK.__REN001.                                                                                        ```
    ```  NOTE: The data set WORK.__REN002 has 2 observations and 2 variables.                                                                                         ```
    ```  NOTE: PROCEDURE TRANSPOSE used (Total process time):                                                                                                         ```
    ```        real time           0.01 seconds                                                                                                                       ```
    ```        cpu time            0.00 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: PROCEDURE SQL used (Total process time):                                                                                                               ```
    ```        real time           0.00 seconds                                                                                                                       ```
    ```        cpu time            0.00 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  NOTE: SQL view WORK.HAVE has been defined.                                                                                                                   ```
    ```  NOTE: PROCEDURE SQL used (Total process time):                                                                                                               ```
    ```        real time           0.00 seconds                                                                                                                       ```
    ```        cpu time            0.00 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  628     set have;                                                                                                                                            ```
    ```  629   run;                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```  NOTE: There were 4 observations read from the data set XPT.HAVE.                                                                                             ```
    ```  NOTE: There were 4 observations read from the data set WORK.HAVE.                                                                                            ```
    ```  NOTE: The data set WORK.WANT has 4 observations and 2 variables.                                                                                             ```
    ```  NOTE: DATA statement used (Total process time):                                                                                                              ```
    ```        real time           5.38 seconds                                                                                                                       ```
    ```        cpu time            0.14 seconds                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

