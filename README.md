# utl-r-grubs-dixon-and-rosner-outlier-tests
Grubs dixon and rosner outlier tests
    %let pgm=utl-r-grubs-dixon-and-rosner-outlier-tests;

    Grubs dixon and rosner outlier tests

    github
    https://tinyurl.com/465nj8ur
    https://github.com/rogerjdeangelis/utl-r-grubs-dixon-and-rosner-outlier-tests

     Three solutions

         1 dixon test    https://statsandr.com/blog/outliers-detection-in-r/#dixons-test
         2 rosner test   https://statsandr.com/blog/outliers-detection-in-r/#rosners-test
         3 grubs test    https://statsandr.com/blog/outliers-detection-in-r/#grubbss-test


    RELATED REPOS
    ---------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-Lund-and-Prescott-tests-for-outliers-in-Bioequivalence
    https://github.com/rogerjdeangelis/utl-grubs-test-for-outliers-using-r-package-outliers
    https://github.com/rogerjdeangelis/utl-outlier-analysis-based-on-robust-regression
    https://github.com/rogerjdeangelis/utl-sas-macro-for-grubs-outlier-analysis
    https://github.com/rogerjdeangelis/utl-univariate-influential-outliers-using-robustreg
    https://github.com/rogerjdeangelis/utl_bivariate_outliers
    https://github.com/rogerjdeangelis/utl_visualizing_suspicious_bivariate_outliers_with_2_dimensional_boxplots

    /********************************************************************************************************************************/
    /*                                |                                             |                                               */
    /*                                |                                             |                                               */
    /*          INPUT                 |        PROCESS                              |    OUTPUT                                     */
    /*                                |                                             |                                               */
    /*       _ _                      | %utl_submit_r64x('                          | R output                                      */
    /*    __| (_)_  _____  _ __       | library(outliers);                          | --------                                      */
    /*   / _` | \ \/ / _ \| `_ \      | library(haven);                             | [1] dixon:                                    */
    /*  | (_| | |>  < (_) | | | |     | have<-read_sas("d:/sd1/have.sas7bdat");     |   Q = 0.6299                                  */
    /*   \__,_|_/_/\_\___/|_| |_|     | temp_file <- tempfile(fileext = ".txt");    |   p-value < 2.2e-16                           */
    /*                                | sink(temp_file);                            |   highest value 5 is an outlier"              */
    /*                                | dixon.test(have$X);                         |                                               */
    /* table SD1.HAVE total obs=30    | sink();                                     | SAS Output                                    */
    /*                                | frame<-as.data.frame(readLines(temp_file)); | ---------                                     */
    /*               X                | frame;                                      | %put &=result                                 */
    /*   5.00000 Outlier              | result<-paste("dixon:",frame[5,],frame[6,]);|                                               */
    /*                                | result;                                     | RESULT=dixon  test:                           */
    /*            1.01525 21  1.39292 | write(result, file = "clipboard");          | Q = 0.65299,                                  */
    /*   0.31757  0.61695 22  1.12294 | ',return=result);                           | p-value < 2.2e-16                             */
    /*   1.98484  2.08891 23  1.67041 |                                             | highest value 5 is an outlier                 */
    /*   1.25616  1.17338 24  0.69110 | %put &=result;                              |                                               */
    /*   0.70101  1.16458 25  1.21829 |                                             |                                               */
    /*   0.55217  0.75245 26  1.11992 |                                             |                                               */
    /*   1.79824  1.61982 27  0.38255 |                                             |                                               */
    /*   0.79484  0.39606 28  0.70527 |                                             |                                               */
    /*   0.87070  0.08878 29  1.15540 |                                             |                                               */
    /*   0.41052  0.80659 30  1.19572 |                                             |                                               */
    /*                                |                                             |                                               */
    /*  libname sd1 "d:/sd1";         |                                             |                                               */
    /*  options validvarname=upcase;  |                                             |                                               */
    /*  data sd1.have;                |                                             |                                               */
    /*    call streaminit(54321);     |                                             |                                               */
    /*    x=5;                        |                                             |                                               */
    /*    output;  * outlier;         |                                             |                                               */
    /*    do i=1 to 29;               |                                             |                                               */
    /*      x=rand('normal',01,.5);   |                                             |                                               */
    /*      output;                   |                                             |                                               */
    /*    end;                        |                                             |                                               */
    /*    drop i;                     |                                             |                                               */
    /*  run;quit;                     |                                             |                                               */
    /*                                |                                             |                                               */
    /*--------------------------------|---------------------------------------------|-----------------------------------------------*/
    /*  _ __ ___  ___ _ __   ___ _ __ |                                             |                                               */
    /* | `__/ _ \/ __| `_ \ / _ \ `__|| %utl_submit_r64x('                          | R                                             */
    /* | | | (_) \__ \ | | |  __/ |   | library(outliers);                          |                                               */
    /* |_|  \___/|___/_| |_|\___|_|   | library(haven);                             | > result                                      */
    /*                                | rosner<-read_sas("d:/sd1/rosner.sas7bdat"); | outlier: highest value 5 is an outlier        */
    /*       SAME INPUT               | test <- grubbs.test(rosner$X);              | p_value: 0.00549671485244985                  */
    /*                                | str(test);                                  |                                               */
    /*                                | result<- paste( "grubs outlier: "           | SAS                                           */
    /*                                |   ,test$alternative                         |                                               */
    /*                                |   ," p_value: ",test$p.value );             | grubs outlier:                                */
    /*                                | result ;                                    |  highest value 5 is an outlier                */
    /*                                | write(result, file = "clipboard");          | p_value:  0.0073675212601938                  */
    /*                                | ',return=result);                           |                                               */
    /*                                |                                             |                                               */
    /*--------------------------------|---------------------------------------------|-----------------------------------------------*/
    /*                   _            |                                             |                                               */
    /*   __ _ _ __ _   _| |__  ___    | Best sample size is large > 20.             | R                                             */
    /*  / _` | `__| | | | `_ \/ __|   |  Can request the number of outliers.        |                                               */
    /* | (_| | |  | |_| | |_) \__ \   |                                             | Results of Outlier Test                       */
    /*  \__, |_|   \__,_|_.__/|___/   | %utl_submit_r64x('                          | -------------------------                     */
    /*  |___/                         | library(EnvStats);                          |                                               */
    /*        SASE INPUT              | library(haven);                             | Test Method:          Rosner's Test           */
    /*                                | rosner<-read_sas("d:/sd1/rosner.sas7bdat"); |                                               */
    /*                                | test <- rosnerTest(rosner$X,k = 1);         | Distribution:         Normal                  */
    /*                                | str(test);                                  |                                               */
    /*                                | val<-test[["all.stats"]]$Value;             | Data:                 rosner$X                */
    /*                                | zscore<-test[["all.stats"]]$R;              |                                               */
    /*                                | pval <- pnorm(zscore, lower.tail=FALSE);    | Sample Size:          31                      */
    /*                                | result=paste(                               |                                               */
    /*                                |   "value:",as.character(val)                | Test Statistic:       R.1 = 3.179687          */
    /*                                |  ,"zscore:",as.character(zscore)            |                                               */
    /*                                |  ,"pval:",as.character(pval));              | Statistic Parameter:  k = 1                   */
    /*                                | result;                                     |                                               */
    /*                                | val;                                        | Alt Hypothesis:       1 observations  not     */
    /*                                | zscore;                                     |                       from the Distribution.  */
    /*                                | pval;                                       |                                               */
    /*                                | test;                                       | Type I Error:         5%                      */
    /*                                | str(result);                                |                                               */
    /*                                | write(result, file = "clipboard");          | Number of Outliers Detected:     1            */
    /*                                | ',return=result)                            |                                               */
    /*                                |                                             |   i   Mean.i     SD.i Value                   */
    /*                                | %put &=result;                              | 1 0 1.112968 1.222457     5                   */
    /*                                |                                             |                                               */
    /*                                |                                             | Obs.Num    R.i+1 lambda.i+1 Outlier           */
    /*                                |                                             |       1 3.179687   2.923571    TRUE           */
    /*                                |                                             |                                               */
    /*                                |                                             |                                               */
    /*                                |                                             | SAS                                           */
    /*                                |                                             |                                               */
    /*                                |                                             | %put &=result;                                */
    /*                                |                                             |                                               */
    /*                                |                                             | RESULT=                                       */
    /*                                |                                             |   value: 5                                    */
    /*                                |                                             |   zscore: 3.17968712287943                    */
    /*                                |                                             |   pval: 0.000737170724902093                  */
    /*                                |                                             |                                               */
    /********************************************************************************************************************************/


    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    libname sd1 "d:/sd1";
    options validvarname=upcase;
    data sd1.have;
      call streaminit(54321);
      x=5;
      output;  * outlier;
      do i=1 to 29;
        x=rand('normal',01,.5);
        output;
      end;
      drop i;
    run;quit;

    /*       _ _
    / |   __| (_)_  _____  _ __
    | |  / _` | \ \/ / _ \| `_ \
    | | | (_| | |>  < (_) | | | |
    |_|  \__,_|_/_/\_\___/|_| |_|

    https://statsandr.com/blog/outliers-detection-in-r/#dixons-test
    */

    Note that R will throw an error and accepts only a dataset consisting of 3 to 30
    observations for this test.

    test whether a single low or high value is an outlier most useful for
    small samples

    dixon.test(x, opposite = TRUE)  * single low value probleml

    /*----                             ----*/
    /*----  test for single high value ----*/
    /*----                             ----*/

    %utl_submit_r64x('
    library(outliers);
    library(haven);
    have<-read_sas("d:/sd1/have.sas7bdat");
    temp_file <- tempfile(fileext = ".txt");
    sink(temp_file);
    dixon.test(have$X);
    sink();
    frame<-as.data.frame(readLines(temp_file));
    frame;
    result<-paste("dixon:",frame[5,],frame[6,]);
    result;
    write(result, file = "clipboard");
    ',return=result);

    %put &=result;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* [1] "dixon test: Q = 0.65299, p-value < 2.2e-16 : alternative hypothesis: highest value 5 is an outlier"               */
    /*                                                                                                                        */
    /* RESULT=dixony test: Q = 0.65299, p-value < 2.2e-16 alternative hypothesis: highest value 5 is an outlier               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___
    |___ \   _ __ ___  ___ _ __   ___ _ __
      __) | | `__/ _ \/ __| `_ \ / _ \ `__|
     / __/  | | | (_) \__ \ | | |  __/ |
    |_____| |_|  \___/|___/_| |_|\___|_|

    https://statsandr.com/blog/outliers-detection-in-r/#rosners-test
    */

    Best sample size is large > 20.
     Can request the number of outliers.

    %utl_submit_r64x('
    library(EnvStats);
    library(haven);
    rosner<-read_sas("d:/sd1/rosner.sas7bdat");
    test <- rosnerTest(rosner$X,k = 1);
    str(test);
    val<-test[["all.stats"]]$Value;
    zscore<-test[["all.stats"]]$R;
    pval <- pnorm(zscore, lower.tail=FALSE);
    result=paste(
      "rosner:"
     ,"value:",as.character(val)
     ,"zscore:",as.character(zscore)
     ,"pval:",as.character(pval));
    result;
    val;
    zscore;
    pval;
    test;
    str(result);
    write(result, file = "clipboard");
    ',return=result)

    %put &=result;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Results of Outlier Test                                                                                                */
    /* -------------------------                                                                                              */
    /*                                                                                                                        */
    /* Test Method:                     Rosner's Test for Outliers                                                            */
    /*                                                                                                                        */
    /* Hypothesized Distribution:       Normal                                                                                */
    /*                                                                                                                        */
    /* Data:                            rosner$X                                                                              */
    /*                                                                                                                        */
    /* Sample Size:                     31                                                                                    */
    /*                                                                                                                        */
    /* Test Statistic:                  R.1 = 3.179687                                                                        */
    /*                                                                                                                        */
    /* Test Statistic Parameter:        k = 1                                                                                 */
    /*                                                                                                                        */
    /* Alternative Hypothesis:          Up to 1 observations are not                                                          */
    /*                                  from the same Distribution.                                                           */
    /*                                                                                                                        */
    /* Type I Error:                    5%                                                                                    */
    /*                                                                                                                        */
    /* Number of Outliers Detected:     1                                                                                     */
    /*                                                                                                                        */
    /*   i   Mean.i     SD.i Value Obs.Num    R.i+1 lambda.i+1 Outlier                                                        */
    /* 1 0 1.112968 1.222457     5       1 3.179687   2.923571    TRUE                                                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* RESULT=value: 5 zscore: 3.17968712287943 pval: 0.000737170724902093                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                    _
    |___ /    __ _ _ __ _   _| |__  ___
      |_ \   / _` | `__| | | | `_ \/ __|
     ___) | | (_| | |  | |_| | |_) \__ \
    |____/   \__, |_|   \__,_|_.__/|___/
             |___/

    https://statsandr.com/blog/outliers-detection-in-r/#grubbss-test
    */

    test detects one outlier at a time (highest or lowest value)

    %utl_submit_r64x('
    library(outliers);
    library(haven);
    rosner<-read_sas("d:/sd1/rosner.sas7bdat");
    test <- grubbs.test(rosner$X);
    str(test);
    result<- paste( "grubs outlier: "
      ,test$alternative
      ," p_value: ",test$p.value );
    result;
    write(result, file = "clipboard");
    ',return=result);

    %put &=result;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  > result                                                                                                              */
    /*  [1] "outlier:  highest value 5 is an outlier  p_value:  0.00549671485244985"                                          */
    /*                                                                                                                        */
    /*  RESULT=grubs outlier:  highest value 5 is an outlier  p_value:  0.0073675212601938                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

