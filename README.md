# utl-symbolically-solve-for-the-mean-and-variance-of-normal-density-using-expected-values-in-SymPy
Symbolically solve for the mean and variance of normal density using expected values in SymPy 
    %let pgm=utl-symbolically-solve-for-the-mean-and-variance-of-normal-density-using-expected-values-in-SymPy;

    Symbolically solve for the mean and variance of normal density using expected values in SymPy

      Two solutions

        1 theory
        2 sympy

    github
    https://tinyurl.com/ms47ndd8
    https://github.com/rogerjdeangelis/utl-symbolically-solve-for-the-mean-and-variance-of-normal-density-using-expected-values-in-SymPy

    /*   _   _
    / | | |_| |__   ___  ___  _ __ _   _
    | | | __| `_ \ / _ \/ _ \| `__| | | |
    | | | |_| | | |  __/ (_) | |  | |_| |
    |_|  \__|_| |_|\___|\___/|_|   \__, |
                                   |___/
    */
    The mean of a normal disribution is defined
    as the expectation ox or integral of
    x*normal pdf from -oo to +oo and the variance


                  oo
                 /
                /              2
               |     -(-mu + x)
               |   ------------
               |           2
               |    2*sigma
               | x*e
     E(x)  =   | ---------------- dx
               |   _____________
              /  \/2 * pi *sigma
             /
             -oo

    Integrating we  get

    E(x) = mu (the mean)


    The variance is defined as

                            oo
                           /
                          /                2
                         |       -(-mu + x)
                         |     ------------
                         |             2
                         |  2   2*sigma               2
        2        2       | x   e                - E(x)
     E(X ) - E(x)   =    | ---------------- dx
                         |   _____________
                        /  \/2 * pi *sigma
                       /
                       -oo


       2        2                    2
    E(X ) - E(x)   = variance = sigma

    /*___
    |___ \   _ __  _ __ ___   ___ ___  ___ ___   ___ _   _ _ __ ___  _ __  _   _
      __) | | `_ \| `__/ _ \ / __/ _ \/ __/ __| / __| | | | `_ ` _ \| `_ \| | | |
     / __/  | |_) | | | (_) | (_|  __/\__ \__ \ \__ \ |_| | | | | | | |_) | |_| |
    |_____| | .__/|_|  \___/ \___\___||___/___/ |___/\__, |_| |_| |_| .__/ \__, |
            |_|                                      |___/          |_|    |___/
    */

    %utl_pybegin;
    parmcards4;
    import sympy as sp
    from sympy import symbols, integrate, exp, sqrt, pi, Eq, solve, pprint, oo
    x, mu, sigma = symbols('x mu sigma', real=True, positive=True)
    normal_pdf = 1/(sigma*sqrt(2*pi)) * exp(-(x - mu)**2 / (2*sigma**2))
    #pprint(x*normal_pdf);
    mean_expr = integrate(x * normal_pdf, (x, -oo, oo))
    print(f"Mean (mu) = {mean_expr}")
    second_moment = integrate(x**2 * normal_pdf, (x, -oo, oo))
    variance = second_moment - mu**2
    print(f"Population Variance = {variance}")
    ;;;;
    %utl_pyend;


    Lets check using a mu=1 and sigma=2(variance=4) and
    gernerating a a million random realizations from

                          oo
                         /
                        /              2
                       |     -(-1  + x)
                       |   ------------
                       |        2
                       |    2*2
                       |   e
    n(mu=1,sigma=2) =  | ---------------- dx
                       |   _____________
                      /  \/2 * pi *2
                     /
                     -oo

    data have;
      call streaminit(4321);
      do i=1 to 1e6;
        x=rand('normal',1,2);
        output;
      end;
      drop i;
      stop;
    run;quit;

    proc means data=have vardef=N mean variance;
    run;quit;

    The mean and variance are very close to 1 and 4

    The MEANS Procedure

       Analysis Variable : X

            Mean        Variance
    ----------------------------
       0.9962963       3.9996237
    ----------------------------

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    Mean (mu) = mu
    Population Variance = sigma**2

    n(mu=1,sigma=2)

    Verification


            Mean        Variance
    ----------------------------
       0.9962963       3.9996237
    ----------------------------

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
