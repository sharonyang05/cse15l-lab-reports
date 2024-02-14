# lab 5 report :)

## pt 1

**input**
```
class CheckString implements StringChecker {
    CheckString() { }
    public boolean checkString(String s) {
        if (s.contains("app")) {
            return true;
        } else {
        return false;
        }
    }
}

public class ListTests {
    
    @Test
    public void testFilterFails() {
        List<String> arr = new ArrayList<>();
        arr.add("application");
        arr.add("apple");
        arr.add("orange");
        arr.add("icon");
        arr.add("pineapple");

        StringChecker sc = new CheckString();

        List<String> filteredArr = ListExamples.filter(arr, sc);

        List<String> expectedArr = new ArrayList<>();
        expectedArr.add("application");
        expectedArr.add("apple");
        expectedArr.add("pineapple");

        assertEquals(expectedArr, filteredArr);
    }

    @Test
    public void testFilterPasses() {
        List<String> arr = new ArrayList<>();
        arr.add("application");
        arr.add("orange");
        arr.add("icon");

        StringChecker sc = new CheckString();

        List<String> filteredArr = ListExamples.filter(arr, sc);

        List<String> expectedArr = new ArrayList<>();
        expectedArr.add("application");

        assertEquals(expectedArr, filteredArr);
    }
}
```
**symptom**
![Image](lab5report-junittests.png)
![Image](lab5report-failedtest.png)

**bug**
original method
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```
fixed ver.
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }
```

The desired output of the `filter()` method is a new list of strings that fit the StringChecker's criteria, in order of appearance in the inputted list of strings. The original line of code where a string is added to the new list, however, adds the string at index 0, causing it to be prepended and reversing the order. (This is also why the input with only one string fitting the StringChecker's criteria seemingly produces no error.) Removing the index parameter from the `add()` call causes it to default to appending the given element, fixing the order.

## pt 2

**option 1: -r**

- search recursively through a directory for a pattern
- useful when wanting to search the contents of an entire directory down all sub-levels without specifying the specific files

example 1: searches all files within `government` for the pattern "Californian" and returns the lines where it appears
```
$ grep -r "Californian" technical/government
technical/government/Media/Bridging_legal_aid_gap.txt:million poor Californians whose basic civil legal needs -- often
technical/government/Media/Bridging_legal_aid_gap.txt:resources so that all Californians, regardless of income, have
technical/government/Media/Bridging_legal_aid_gap.txt:all Californians. In 1999, thanks to Gov. Gray Davis and leaders in
technical/government/Media/Bridging_legal_aid_gap.txt:Californians spend on lawyers each year -- and that 2 percent would
technical/government/Media/Bridging_legal_aid_gap.txt:that the goal of equal access to justice for all Californians is
technical/government/Media/Few_who_need.txt:the legal needs of low-income Californians.
technical/government/Media/Few_who_need.txt:every 10,000 poor Californians. Despite this bleak picture, the
technical/government/Media/Free_Legal_Assistance.txt:more Californians are going to court without a lawyer.
technical/government/Media/Lockyer_Warns.txt:State Atty. Gen. Bill Lockyer is warning Californians to beware
```

example 2: searches all files within `plos` for the pattern "trauma" and returns the lines where it appears
```
$ grep -r "trauma"  technical/plos/
technical/plos/journal.pbio.0020046.txt:        damage, e.g., stroke, intracerebral hemorrhage, or head trauma. It is a rare phenomenon
technical/plos/journal.pbio.0020046.txt:        Given reports on acquired stuttering after brain trauma (Grant et al. 1999; Ciabarra et    
technical/plos/journal.pbio.0020430.txt:        restoring motor function after traumatic lesion of the central nervous system. The current 
technical/plos/pmed.0020007.txt:        good vascular health, physical exercise, and avoidance of head trauma. But there is no
technical/plos/pmed.0020019.txt:        two halves of her face. She was a nonsmoker and denied any history of head or neck trauma,
technical/plos/pmed.0020086.txt:        those influences that are modifiable. Controlling blood pressure and avoiding head trauma
```


**option 2: -i**

- ignore case when searching for the pattern
- useful when searching for a word where capitalization/location within a sentence is arbitrary

example 1: searches `1468-6708-3-10.txt` for any line where the word heart appears and returns them
```
$ grep -i "heart" technical/biomed/1468-6708-3-10.txt
        Prevent Heart Attack Trial (ALLHAT) is a randomized,
        Heart, Lung, and Blood Institute (NHLBI). A double-blind,
        compare the rate of fatal coronary heart disease (CHD) or
        National Heart, Lung, and Blood Institute accepted a
        outpatient], heart failure [HF/treated in the hospital or
          Heart Failure Diagnosis
          nocturnal dyspnea, dyspnea at rest, New York Heart
          either of these alone, without other indications of heart
          Heart Failure Diagnostic Criteria
        1) New York Heart Classification functional class III:
        Assessment of Patients with Diseases of the Heart: AHA
```

example 2: searches `Session2-PDF.txt` for any line where the word alcoholism appears and returns them
```
$ grep -i "alcoholism"  technical/government/Alcohol_Problems/Session2-PDF.txt
Institute on Alcohol Abuse and Alcoholism (NIAAA) defines at-risk
SAAST (Self-Administered Alcoholism Screening Test) was
4. National Institute on Alcohol Abuse and Alcoholism. The
the CAGE, the Brief Michigan Alcoholism Screening Test, and the
center patients for alcoholism. J Trauma 1997;43:962-9.
questions in the detection of alcoholism. JAMA 1988;259:51-4.
19. Fleming M, Barry K. The effectiveness of alcoholism
for alcoholism. J Gen Intern Med 1990;5:361-4.
24. Ewing J. Detecting alcoholism: the CAGE questionnaire.
version of the Michigan Alcoholism Screening Test. Am J Psychiatry
27. Selzer M. The Michigan Alcoholism Screening Test: the quest
Short Michigan Alcoholism Screening Test (SMAST). J Stud Alcohol
analysis of the Self-Administered Alcoholism Screening Test.
30. Davis L, Jr., Morse R. Self-Administered Alcoholism
center patients for alcoholism. J Trauma 1997; 43:962-9.
Alcoholism. Criteria for the diagnosis of alcoholism. Am J
alcoholism in primary health care: compared efficacy of different
criterion-oriented validation of an alcoholism questionnaire in
Alcoholism screening in the elderly. J Am Geriatr Soc
H. Identification of alcoholism and depression in a geriatric
```

**option 3: -l**
- return the name of any file where a particular pattern appears
- useful for a broader search for any files containing a pattern/keyword

example 1: searches `government` for any files containing the pattern "Canada" and returns the file names
```
$ grep -l -r "Canada" technical/government/
technical/government/About_LSC/ONTARIO_LEGAL_AID_SERIES.txt
technical/government/About_LSC/Progress_report.txt
technical/government/About_LSC/Strategic_report.txt
technical/government/Env_Prot_Agen/atx1-6.txt
technical/government/Env_Prot_Agen/ctf1-6.txt
technical/government/Env_Prot_Agen/ctm4-10.txt
technical/government/Env_Prot_Agen/multi102902.txt
technical/government/Env_Prot_Agen/ro_clear_skies_book.txt
technical/government/Gen_Account_Office/ai00134.txt
technical/government/Gen_Account_Office/ai9868.txt
technical/government/Gen_Account_Office/d01376g.txt
technical/government/Gen_Account_Office/d01591sp.txt
technical/government/Gen_Account_Office/d0269g.txt
technical/government/Gen_Account_Office/gg96118.txt
technical/government/Gen_Account_Office/May1998_ai98068.txt
technical/government/Gen_Account_Office/Oct15-2001_d0224.txt
technical/government/Gen_Account_Office/pe1019.txt
technical/government/Media/Assuring_Underprivileged.txt
technical/government/Media/Few_who_need.txt
technical/government/Post_Rate_Comm/Cohenetal_comparison.txt
technical/government/Post_Rate_Comm/Cohenetal_Cost_Function.txt
technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt
technical/government/Post_Rate_Comm/Redacted_Study.txt
```

example 2: searches `technical/biomed/` recursively for every file containing the words "stem cell" (ignoring case) and return them
```
sysha@LAPTOP-QNTF4H98 MINGW64 ~/OneDrive/1 UCSD Year 1/CSE 15L/lab 5/docsearch (main)
$ grep -l -r -i "stem cell" technical/biomed/
technical/biomed/1471-213X-1-1.txt
technical/biomed/1471-213X-1-10.txt
technical/biomed/1471-213X-1-11.txt
technical/biomed/1471-213X-1-12.txt
technical/biomed/1471-213X-2-8.txt
technical/biomed/1471-2164-4-22.txt
technical/biomed/1471-2210-2-4.txt
technical/biomed/1471-230X-1-10.txt
technical/biomed/1471-2407-2-12.txt
technical/biomed/1471-2407-2-15.txt
technical/biomed/1471-2474-2-2.txt
technical/biomed/1472-6874-2-8.txt
technical/biomed/1472-6890-1-4.txt
technical/biomed/1477-7827-1-36.txt
technical/biomed/1477-7827-1-46.txt
technical/biomed/ar130.txt
technical/biomed/ar309.txt
technical/biomed/ar745.txt
technical/biomed/bcr285.txt
technical/biomed/cvm-2-6-278.txt
technical/biomed/gb-2001-2-11-research0045.txt
technical/biomed/gb-2002-3-5-research0025.txt
technical/biomed/gb-2003-4-7-r46.txt
```

**option 4: -n**
- returns the line number of the line a pattern appears in
- useful when trying to find the exact location of a pattern in a file

example 1: searches `1472-6963-3-7.txt` for lines containing the pattern "ulcer" and returns the line + line number of its appearance
```
$ grep -n "ulcer" technical/biomed/1472-6963-3-7.txt
422:            Neuropathy and foot ulcers can lead to amputations.
475:            For the purpose of this analysis, foot ulcers are
477:            vascular surgery. Since not all diabetic foot ulcers
483:            diabetic foot ulcer is $2,183 per person, on average.
581:        likely that the foot ulcer, LEA and symptomatic neuropathy
```

example 2: searches `technical/` recursively for the pattern "Vancouver" and returns the file name + line number + line of its appearance
```
$ grep -n -r "Vancouver" technical/
technical/911report/chapter-6.txt:150:                but he did not get a reply. He spent a week in Vancouver preparing the explosive
technical/911report/chapter-6.txt:155:            While in Vancouver, Ressam also rented a Chrysler sedan for his travel into the
technical/biomed/1475-925X-2-10.txt:395:            tablet (Intuos, Wacom Corp., Vancouver, WA) an ellipse
technical/biomed/rr167.txt:143:          patients with CF in Vancouver, Canada, kindly provided by
technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt:22:University, Vancouver, Canada, June 710, 2000 2 The writer is
technical/plos/journal.pbio.0020113.txt:129:        Daniel Pauly, a fisheries biologist at the University of Vancouver (Vancouver, British 
```
