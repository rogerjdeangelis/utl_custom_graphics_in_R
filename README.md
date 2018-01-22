# utl_custom_graphics_in_R
Custom graphics in R.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Custom graphics in R

    github graphics
    https://goo.gl/ij19Ni
    https://github.com/rogerjdeangelis/utl_custom_graphics_in_R/blob/master/utl_custom_graphics_in_R_2.pdf

    https://goo.gl/NXFcrm
    https://github.com/rogerjdeangelis/utl_custom_graphics_in_R/blob/master/utl_custom_graphics_in_R_1.pdf

    project
    https://github.com/rogerjdeangelis/utl_custom_graphics_in_R

     WPS Proc R

       Two Examples
          1. Simple base graphic
          2. More comples ggplot2 graphic

    StackOverflow
    https://stackoverflow.com/questions/48323643/custom-graphics-in-r

    Profiles

    Bernhard
    https://stackoverflow.com/users/6503141/bernhard

    Claus Wilke
    https://stackoverflow.com/users/4975218/claus-wilke


    HAVE
    ====
      Data and functions in the R script

       line functions
       arrow symbols
       polygon functions


    WANT (high res graphic below)
    =============================

       Risk and Reward

        Lower Risk                    Upper Risk
       <---------------------------------------->

       Typical Low Rewards   Typical High Rewards

       +-----+-----+-----+-----+-----+-----+-----+
       |     |     |     |     |     |     |     |
       |  1  |  2  |  3  |  4  |  5  |  6  |  7  |
       |     |     |     |     |     |     |     |
       +-----+-----+-----+-----+-----+-----+-----+
                                         ^
                                        /#\
                                         |
                                         |
    PROCESS (all the code)
    =======================
     1. Using Base R graphics (all the code)

        %utl_submit_wps64('
        libname sd1 sas7bdat "d:/sd1";
        options set=R_HOME "C:/Program Files/R/R-3.3.2";
        proc r;
        submit;
        library(rsvg);
        source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
        draw <- function(x){
            plot(NA, xlim=c(0,7), ylim=c(-.3,1), xaxt="n", yaxt="n", xlab="", ylab="");
            lines(x=c(0,0,1,1,2,2,3,3,4,4,5,5,6,6,7,7,0),
                  y=rep(c(0,1,1,0,0,1,1,0,0,1,1,0,0,1,1,0,0)));
            lines(c(0,7),c(1,1));
            for(i in 1:7) text(x = i-0.5, y= 0.5, labels=i);
            arrows(0, 1.5, 7, 1.5, code=3);
            polygon(x -1 +c(-.1, 0, .1),c(-.3,-0.05,-.3), col="black");
        };
        pdf("d:/pdf/utl_custom_graphics_in_R_1.pdf");
        draw(4);
        draw(3);
        endsubmit;
        run;quit;
        ');


     2. ggplot2

        %utl_submit_wps64('
        libname sd1 sas7bdat "d:/sd1";
        options set=R_HOME "C:/Program Files/R/R-3.3.2";
        proc r;
        submit;
        library(ggplot2);
        source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
        df_nums <- data.frame(number <- 1:7,
          fill <- c(rep("white", 5), "darkblue", "white"),
          color <- c(rep("black", 5), "white", "black"));
        df_text <- data.frame(label = c("Lower Risk", "Higher Risk", "Typically Lower Rewards",
           "Typically Higher Rewards"),
           hjust = c(0, 1, 0, 1),
           x = c(0, 7, 0, 7),
           y = c(2.9, 2.9, 2.1, 2.1));
        arrow_x_pos <- 6.8;
        p1 <- ggplot(df_nums) +
          geom_tile(aes(x = number - .5, y = 1, fill = fill), size = 1, color = "black") +
          geom_text(aes(x = number - .5, y = 1, color = color, label = number), size = 8) +
          scale_color_identity(guide = "none") + scale_fill_identity(guide = "none") +
          geom_text(data = df_text, aes(x = x, y = y, label = label, hjust = hjust), size = 5.5,
                    fontface = "bold") +
          geom_text(aes(label = "Risk and Reward Profile", x = 0, y = 3.5),
                    fontface = "bold", size = 6.5, hjust = 0) +
          geom_segment(x = 0, xend = 7, y = 2.5, yend = 2.5, size = 1,
                       arrow = arrow(length = unit(10,"pt"), ends = "both"),
                       color = "grey70") +
          geom_segment(x = arrow_x_pos - 1, xend = arrow_x_pos - 1, y = -.3, yend = .2, size = 4,
                       arrow = arrow(length = unit(7, "pt"), type = "closed"),
                       lineend = "butt", linejoin = "mitre") +
          ylim(-.2, 3.6) +
          coord_fixed() +
          theme_void();
        pdf("d:/pdf/utl_custom_graphics_in_R_2.pdf");
        p1;
        endsubmit;
        run;quit;
        ');

     *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

      all the data is in the R scripts

     *_                                            _     _
    | |__   __ _ ___  ___    __ _ _ __ __ _ _ __ | |__ (_) ___ ___
    | '_ \ / _` / __|/ _ \  / _` | '__/ _` | '_ \| '_ \| |/ __/ __|
    | |_) | (_| \__ \  __/ | (_| | | | (_| | |_) | | | | | (__\__ \
    |_.__/ \__,_|___/\___|  \__, |_|  \__,_| .__/|_| |_|_|\___|___/
                            |___/          |_|
    ;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    proc r;
    submit;
    library(rsvg);
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    draw <- function(x){
        plot(NA, xlim=c(0,7), ylim=c(-.3,1), xaxt="n", yaxt="n", xlab="", ylab="");
        lines(x=c(0,0,1,1,2,2,3,3,4,4,5,5,6,6,7,7,0),
              y=rep(c(0,1,1,0,0,1,1,0,0,1,1,0,0,1,1,0,0)));
        lines(c(0,7),c(1,1));
        for(i in 1:7) text(x = i-0.5, y= 0.5, labels=i);
        arrows(0, 1.5, 7, 1.5, code=3);
        polygon(x -1 +c(-.1, 0, .1),c(-.3,-0.05,-.3), col="black");
    };
    pdf("d:/pdf/ruler.df");
    draw(4);
    draw(3);
    endsubmit;
    run;quit;
    ');

    *                  _       _   ____
      __ _  __ _ _ __ | | ___ | |_|___ \
     / _` |/ _` | '_ \| |/ _ \| __| __) |
    | (_| | (_| | |_) | | (_) | |_ / __/
     \__, |\__, | .__/|_|\___/ \__|_____|
     |___/ |___/|_|
    ;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    proc r;
    submit;
    library(ggplot2);
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    df_nums <- data.frame(number <- 1:7,
                          fill <- c(rep("white", 5), "darkblue", "white"),
                          color <- c(rep("black", 5), "white", "black"));
    df_text <- data.frame(label = c("Lower Risk", "Higher Risk", "Typically Lower Rewards",
                                    "Typically Higher Rewards"),
                          hjust = c(0, 1, 0, 1),
                          x = c(0, 7, 0, 7),
                          y = c(2.9, 2.9, 2.1, 2.1));
    arrow_x_pos <- 6.8;
    p1 <- ggplot(df_nums) +
      geom_tile(aes(x = number - .5, y = 1, fill = fill), size = 1, color = "black") +
      geom_text(aes(x = number - .5, y = 1, color = color, label = number), size = 8) +
      scale_color_identity(guide = "none") + scale_fill_identity(guide = "none") +
      geom_text(data = df_text, aes(x = x, y = y, label = label, hjust = hjust), size = 5.5,
                fontface = "bold") +
      geom_text(aes(label = "Risk and Reward Profile", x = 0, y = 3.5),
                fontface = "bold", size = 6.5, hjust = 0) +
      geom_segment(x = 0, xend = 7, y = 2.5, yend = 2.5, size = 1,
                   arrow = arrow(length = unit(10,"pt"), ends = "both"),
                   color = "grey70") +
      geom_segment(x = arrow_x_pos - 1, xend = arrow_x_pos - 1, y = -.3, yend = .2, size = 4,
                   arrow = arrow(length = unit(7, "pt"), type = "closed"),
                   lineend = "butt", linejoin = "mitre") +
      ylim(-.2, 3.6) +
      coord_fixed() +
      theme_void();
    pdf("d:/pdf/utl_custom_graphics_in_R.pdf");
    p1;
    endsubmit;
    run;quit;
    ');

