# Lab Report 3


## Part 1 - Bugs
I chose to use the bug found in ArrayExamples.java file in the reverseInPlace method. 

In the starter code, when we ran the JUnit Tests, a failure-inducing input was basically any array with size greater than 1. 

An example of a failure-inducing input was this test:

```
@Test 
  public void testReverseInPlaceFail(){
    int[] input1 = {1,2,3,4,5};
    ArrayExamples.reverseInPlace(input1);
    int[] expected = {5,4,3,2,1};
    assertArrayEquals(expected, input1);
  }
```

Once it got to the midpoint of the array it continued to the second half of the array and reversed it again. 

An example of an input that doesn't induce a failure is:
```
@Test
  public void testReverseInPlacePass(){
    int[] input1 = {1};
    ArrayExamples.reverseInPlace(input1);
    int[] expected = {1};
    assertArrayEquals(expected, input1);
  }
```

Here is the symptom from running both tests: 


The code originally was this: 
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
To fix the bug, I changed it to this:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length-i-1] = temp;
    }
  }
```

This allowed us to store the value of the index before it gets swapped, so its counterpart could then hold that value. For example, say we have a list with an array size of 5. And we wanted to swap the element at index 0 with the element at index 4. To do this we would have to store the initial element at index 0 in a temporary variable so that when it gets reassigned to the element at index 4, we can then swap the temp variable to be reassigned to index 4. I also changed the for loop to iterate over half the array because we are swapping two lements at a time and iterating over the whole array is going to reverse it twice. 

## Part 2 - Researching Commands

Command of Choice: grep
I found all of these command line options on this webpage: [grep(1) — Linux manual page](https://man7.org/linux/man-pages/man1/grep.1.html)

### grep -c (count)

```
brandonnghiem@Brandons-MacBook-Air-2 biomed % grep -c "Introduction" 1468-6708-3-4.txt
1
```

This shows that in the file 1468-6708-3-4.txt, the word "Introduction" showed up once. This is useful because essentially its a word count. Say we were looking inside a code file, we could essentially look up the frequency of a certain method and how often it is called. 

```
grep -c "Brandon" 1468-6708-3-4.txt          
0
```
This shows that in the file 1468-6708-3-4.txt, the word "Brandon" showed up zero times. This is useful because we can also find out what words aren't in the file. We can also see if certain methods are not in a certain class or file, which is very useful in terms of code tracing. 


### grep -l (outputs files)

```
brandonnghiem@Brandons-MacBook-Air-2 911report % grep -l ":" chapter-1.txt chapter-2.txt chapter-3.txt
chapter-1.txt
chapter-2.txt
chapter-3.txt
```

This command option lists the files that contain the certain pattern. I was looking through the files in 911report and noticed time stamps. So I checked for colons in the first three txt files, and the output given means that all three contain the presence of ":". This is useful in terms of filtering files instead of having the lines printed for the normal grep command. 

```
brandonnghiem@Brandons-MacBook-Air-2 911report % grep -l "9/11" chapter-1.txt chapter-2.txt chapter-3.txt chapter-4.txt chapter-10.txt chapter-9.txt 
chapter-1.txt
chapter-2.txt
chapter-3.txt
grep: chapter-4.txt: No such file or directory
chapter-10.txt
chapter-9.txt
```
I wanted to test what would happen if I gave one file (in a list of files) that didn't exist. This ran through the inputs and outputted the files that contained the pattern "9/11" but it also indicated that chapter-4.txt did not exist in the directory. This is useful because again, it allows for file filtering. 



### grep -L (files without match)

```
brandonnghiem@Brandons-MacBook-Air-2 911report % grep -L ":" chapter-1.txt chapter-2.txt chapter-3.txt                  
brandonnghiem@Brandons-MacBook-Air-2 911report % 
```
This command option "L" is the exact opposite of "l" and it outputs the files that don't contain the pattern. As expected we used the same pattern and file inputs as its counterpart, but this time it ouputted nothing because they all contain ":". This is useful for file filtering. But also, say we had a list of classes that are supposed to implement a certain method. We can use this to find files that don't implement the method and add it in. 


```
grep -L "9/11" chapter-1.txt chapter-2.txt chapter-3.txt chapter-4.txt chapter-10.txt chapter-9.txt
grep: chapter-4.txt: No such file or directory
```
Again, this is the exact opposite compared to when we ran this with "l". And as expected it didn't output all the same files because they do contain "9/11". It also sent us a message that chapter-4.txt has no such file or directory which is useful for distinguishing if files are in the directory. 


### grep -v (selecting non matching lines)

```
brandonnghiem@Brandons-MacBook-Air-2 plos % grep -v "a" journal.pbio.0020001.txt

  
    
      
        
        serious problems not only for the scientific community in the developing countries, but for
        
          
          
        
      
      
        2002).
        
          
          
        
      
      
      
      
        regions.
        In 
        However, publishing in 
      
      
        world.
        
          
          
        
        built.
      
    
  
```
This outputted lines that didn't contain the pattern "a" in journal.pbio.0020001.txt. This could be useful say in a situation where we want to see our code without comments, so we could use grep -v on "//". 

```
brandonnghiem@Brandons-MacBook-Air-2 plos % grep -v "research" journal.pbio.0020001.txt

  
    
      
        
        Kofi Annan, the Secretary-General of the United Nations, recently called attention to
        the clear inequalities in science between developing and developed countries and to the
        challenges of building bridges across these gaps that should bring the United Nations and
        the world scientific community closer to each other (Annan 2003). Mr. Annan stressed the
        importance of reducing the inequalities in science between developed and developing
        countries, asserting that “This unbalanced distribution of scientific activity generates
        serious problems not only for the scientific community in the developing countries, but for
        development itself.” Indeed, Mr. Annan's sentiments have also been echoed recently by
        several scientists, who present overwhelming evidence for the disparity in scientific
        output between the developing and already developed countries (Gibbs 1995; May 1997;
        Goldemberg 1998; Riddoch 2000). For example, recent United Nations Educational, Scientific,
        and Cultural Organization (UNESCO) estimates (UNESCO 2001) indicate that, in 1997, the
        88% of all scientific and technical publications registered by the Science Citation Index
        (SCI). North America and Europe clearly dominate the number of scientific publications
        produced annually, with 36.6% and 37.5%, respectively, worldwide (UNESCO 2001).
        
          
            North America and Europe clearly dominate the number of scientific
            publications produced annually.
          
        
        It is rather obvious that richer countries are able to invest more resources in science
        and therefore account for the largest number of publications. It is also likely that there
        is a statistical bias on the part of the SCI as a bibliometric database, since it
        represents North American and European publications far better than those of the rest of
        the world (Gibbs 1995; May 1997; Alonso and Fernández-Juricic 2001; Vohora and Vohora
        2001). But is the disparity in scientific contributions between the developed and
        developing worlds actually remaining unchanged or even increasing, as Mr. Annan has
        implied? A closer look at the trends over the last decade reveals important advances in
        developing countries. For example, Latin America and China, although representing,
        respectively, only 1.8% and 2% of scientific publications worldwide, have increased the
        number of their publications between 1990 and 1997 by 36% and 70%, respectively, which is a
        much higher percentage than the increments reached by Europe (10%) and industrial Asia
        (26%). The percentage of global scientific publications from North America actually
        decreased by 8% over the same period (UNESCO 2001).
      
      
        Publishing Trends in the Americas
        Using the SCI databases produced by the Institute for Scientific Information (ISI), as
        well as data compiled by the Red Iberoamericana de Indicadores de Ciencia y Tecnología
        (RICYT), we examined the differences in the number and proportion of scientific
        publications between the developed world and the developing world from 1990 until 2000,
        focusing on the Americas as a case study. Not surprisingly, there was a huge disparity in
        the number of publications from 1990 until 2000, with the United States contributing the
        lion's share (84.2%), followed by Canada (10.35%). Latin America as a whole contributed
        only 5.45% to the total number of scientific publications in these ten years (RICYT
        2002).
        The total number of publications, however, is not necessarily the best measure for
        assessing scientific productivity or technical advances (May 1997). More relevant
        measurements for these factors include the proportional change in the number of
        and development (May 1997). The proportional change in the number of publications, using
        1990 as a comparison, revealed that scientific publishing in Latin America increased the
        most rapidly in the Americas, far outpacing the United States and Canada (Figure 1).
        Further analyses, correcting the number of overall publications for the amount of money
        Canada and United States, the trend in Latin America has been an increase in relative
        output throughout the 1990s (Figure 2). Moreover, when taking into account the amount of
        other work standards, these factors do not explain the substantial increase in the number
        particularly from 1995 until 2000 (Figure 2).
        Other relative indicators of scientific productivity, such as the number of publications
        picked up by the SCI in relation to the number of scientists in a particular country, also
        demonstrate that such developing regions as Latin America are making substantial
        contributions to science, despite the fact that the average proportion of gross domestic
        product (GDP) invested in science in Latin America throughout this 10-year period was only
        21% of the amount invested in United States (RICYT 2002). Indeed, this scientific
        productivity is remarkable when we compare it with the relatively low investment in science
        itself as compared with the GDP of Latin America as a whole. In fact, Albornoz (2001)
        concluded that, as a group, Latin America could afford to invest a much higher proportion
        effort compared with that of the United States (2.84%) and Canada (1.5%).
        Among Latin American countries, there is a high degree of variability in publication
        rate as well as in financial investment in science and technology. Some countries have
        performed particularly well. For example, Uruguay, Chile, Panama, and Cuba averaged,
        development investment in the 10 years studied, which is notoriously high compared with
        United States (1.5) and even Canada (3.3) (RICYT 2002). Other countries, such as Costa
        Rica, Cuba, Brazil, and Chile, have invested a much greater proportion of their GDP in
        
          
            development been increasing in Latin America while decreasing in United States and
            Canada?
          
        
      
      
        Explaining the Increase in Publishing Productivity in Latin America
        One potential explanation for the increase in scientific productivity in Latin America
        is that scientific development during the 1990s was particularly strong for many countries
        of this region. Indeed, this would explain the rapid rise in the number of publications in
        Latin America compared with the relatively flat increases in the United States and Canada,
        which were publishing just as well at the beginning of the decade. A potentially more
        important question, however, is why the number of publications per dollar invested in
        United States and Canada. This pattern could be the result of a variety of factors, none of
        which are mutually exclusive. It is possible that publishing in international journals as a
        measure of scientific productivity is becoming more important in Latin America. Increased
        funding to the most productive scientists from the national science development programs
        might have been an important stimulus. International cooperation resulting in more
        scientific collaborations among scientists in Latin America, Europe, and the United States
        may also have increased the relative number of publications in Latin America. In contrast,
        the decreasing trends in the number of publications per investment dollar in Canada and
        programs.
      
      
        Scientific Impact from Latin America
        What, exactly, is the relative impact of such developing regions as Latin America on the
        scientific community? We used SCI 2001 data to examine the proportion of publications in
        the area of ecology (including the fields of evolutionary biology, conservation biology,
        and global change biology) between 1990 and 2002 in both the two top general science
        journals (
        Nature and 
        Science ; with impact factors of 27.96 and 23.33, respectively) and in
        the 20 top ecological journals (with impact factors of 10.51–2.47) (ISI 2001a). We credited
        a region with a publication if any of the authors were affiliated with institutions from
        that region. Thus, more than one region would receive credit for a single publication if
        that publication had been written by multiple authors from institutions of different
        regions.
        For the top 20 ecological journals, the American subcontinents of South, Central, and
        North America accounted for 62% of the publications worldwide. Within the Americas,
        however, Latin America represented only 6%, while Canada and United States accounted,
        respectively, for 13% and 82% of the top 20 ecological publications. When we examined the
        data as contributions to the top 10 ecological journals (impact factors 10.51–3.31) versus
        the top 11–20 (impact factors 3.28–2.47), the Latin American countries contributed nearly
        twice as many publications to journals in the second category (8% in the top 11–20 compared
        with 4% in the top 10). These findings suggest that publications from such developing
        regions as Latin America are falling short of reaching the top journals. In contrast, the
        United States contributed somewhat more publications to the top 10 journals (84%) than the
        top 11–20 journals (79%). The difference in the proportion of publications contributed by
        the United States to the top 10 and top 20 journals was even more pronounced when we
        examined it in respect to worldwide publications. In this case, the United States
        contributed 60% of the publications to the top 10 journals and only 40% of the publications
        to the top 11–20 journals.
        Interestingly, the proportion of publications from Latin America, the United States, and
        Canada across all subject areas in 
        Science and 
        Nature were nearly identical to those of the top 20 ecological journals.
        In 
        Science and 
        Nature , Latin America had 7% of the publications within the Americas
        versus 6% in the top 20 ecological journals, whereas the United States and Canada had 81%
        versus 82% and 12% versus 13%, respectively. These similarities suggest that the Latin
        However, publishing in 
        Science and 
        Nature was not enough to gain prominence, as evidenced by the number of
        ecology and environmental sciences emphasizes the overwhelming contributions of authors
        American institution was included in the remaining 6%. Overall, these data indicate that
        the scientific output in the field of ecology in Latin America is having a relatively low
        impact in the international scientific community and is underrepresented in the top
        international journals, despite its robust productivity as measured by the number of
        (Swinbanks et al. 1997) and thus could be a general phenomenon in the developing world.
        independently are making important contributions to the international scientific community,
        they are the exception. Why, in general, do Latin American scientists often fail to reach
        and that the top journals, which are published in the developed world, respond more to the
        scientific mainstream of the developed regions. This is not to suggest any sort of
        conspiracy, but rather it implies that the perception of the most important science is
        linked to the region and that because the major funding agencies as well as most prominent
        journals share a similar economic region, they also share the same perception of what
        science is most interesting to them. Another consideration is that more local journals from
        developed regions are listed by the SCI than similar journals from developing regions
        (Gibbs 1995). Consequently, there are more high-profile regional publication opportunities
        locally in the developing world is overlooked. But it takes more than publishing good
        papers to become a highly cited scientist. It requires attending international meetings and
      
      
        A Long Road Yet to Travel
        The positive trends in scientific productivity in Latin America should not be
        misinterpreted as a reason to be unconcerned about the existing gap highlighted by Mr.
        Annan. There are many compelling reasons for the push to increase scientific input from the
        developing world (Goldemberg 1998; Annan 2003). One is that science, as a discipline, would
        benefit from the contributions of many disparate groups around the world, rather than being
        dominated by two geographic regions. Many scientific problems could be solved much more
        readily with the cooperation and scientific insight of scientists from developing regions.
        from those developing regions that are so important for these global processes. It is also
        areas of concern that are having a proportionally greater scientific and social impact upon
        Brazil (Goldemberg 1998) and biomedical sciences in Cuba (Castro Díaz-Balart 2002). These
        examples are important not only for those regions of the developing world, but are also in
        themselves scientific innovations that can greatly advance the knowledge of the rest of the
        world.
        
          
            input from those developing regions that are so important for global processes.
          
        
        Although the evidence presented here demonstrates that there is a long way to go before
        developing countries contribute a more equitable share to the international scientific
        community, there are also reasons to be optimistic. The relative increase in the number of
        development, demonstrates that many developing countries are heading in the right
        direction. The extremely high scientific productivity of many developing nations, corrected
        for and despite the rather limited availability of funds, suggests that increased funding
        to the sciences will be an excellent investment by developing nations in terms of
        publications as a measure of scientific output, particularly if these publications can
        target the journals that have the greatest impact. Although there may still be a long road
        to travel, we feel optimistic that the bridges mentioned by Mr. Annan are slowly being
        built.
      
```

This filtered out and ouputted the lines that didn't include the word "research". Another use of this command line option could be filtering out sensitive information such as methods we want to hide or abstract. 




