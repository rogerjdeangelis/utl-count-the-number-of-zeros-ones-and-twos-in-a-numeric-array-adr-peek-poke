# utl-count-the-number-of-zeros-ones-and-twos-in-a-numeric-array-adr-peek-poke
Count the number of zeros ones and twos in a numeric array adr peek poke
    Count the number of zeros ones and twos in a numeric array adr peek poke

          Two Solutions

             1. Cats function (single digit only)
             2, Adr, peek and poke  (handles more cases)


     github
     https://tinyurl.com/y55azccb
     https://github.com/rogerjdeangelis/utl-count-the-number-of-zeros-ones-and-twos-in-a-numeric-array-adr-peek-pok

     *_                   _
     (_)_ __  _ __  _   _| |_
     | | '_ \| '_ \| | | | __|
     | | | | | |_) | |_| | |_
     |_|_| |_| .__/ \__,_|\__|
             |_|
     ;

     data have;
      input x1-x5;
     cards4;
     2 2 2 2 2
     1 0 0 0 0
     1 1 0 0 0
     1 1 0 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 2 2
     ;;;;
     run;quit;
     *            _               _
       ___  _   _| |_ _ __  _   _| |_
      / _ \| | | | __| '_ \| | | | __|
     | (_) | |_| | |_| |_) | |_| | |_
      \___/ \__,_|\__| .__/ \__,_|\__|
                     |_|
     ;
                                   | RULES
     WORK.HAVE total obs=8         |
                                   |
       X1    X2    X3    X4    X5  |  ZRO    ONE    TWO
                                   |
        2     2     2     2     2  |   0      0      5   * 5 Twos
        1     0     0     0     0  |   4      1      0   * 4 Zeros, 1 one
        1     1     0     0     0  |   3      2      0
        1     1     0     0     0  |   3      2      0
        1     1     1     0     0  |   2      3      0
        1     1     1     0     0  |   2      3      0
        1     1     1     0     0  |   2      3      0
        1     1     1     2     2  |   0      3      2

     *
      _ __  _ __ ___   ___ ___  ___ ___
     | '_ \| '__/ _ \ / __/ _ \/ __/ __|
     | |_) | | | (_) | (_|  __/\__ \__ \
     | .__/|_|  \___/ \___\___||___/___/
     |_|
     ;



     ********************
     1. Cats function   *
     ********************

     data have;
      input x1-x5;
     cards4;
     2 2 2 2 2
     1 0 0 0 0
     1 1 0 0 0
     1 1 0 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 2 2
     ;;;;
     run;quit;

     data want;

       set have;

       cs = cats(of x:);

       zro=count(cs,'0');
       one=count(cs,'1');
       two=count(cs,'2');

       drop cs;

     run;quit;



     ***********************************************
     2, Adr, peek and poke  (handles more cases)   *
     ***********************************************

     data have;
      input x1-x5;
     cards4;
     2 2 2 2 2
     1 0 0 0 0
     1 1 0 0 0
     1 1 0 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 0 0
     1 1 1 2 2
     ;;;;
     run;quit;

     data want;

       array xs[*] x1-x5;

       set have;

       length cs $40;

       * move the numeric array into a string;

       call pokelong( peekclong(addrlong(xs[1]),40), addrlong(cs), 40 );

       zro=count(cs,put(0,rb8.));
       one=count(cs,put(1,rb8.));
       two=count(cs,put(2,rb8.));

       drop cs;

     run;quit;



