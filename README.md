# WorlListSolution
Reads a sorted list-longest word first
Breaks the word to substrings-to the length of the word
compares each element from the list of substrings if it exists in the List of Words
If the elements form words that are part of the word list, then passes it.
Gives out a list of 62260 such words.

Commented code is tried to work with different objects to check performance.
1. Longest word immunoelectrophoretically,
2. second longes word phosphatidylethanolamines 
3.62260 words possible.



using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.IO;

namespace WebApplication14
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            string[] wordList = File.ReadAllLines("C:\\WebApplication14\\WebApplication14\\Scripts\\Test.txt");
            

            List<string> LongestWord = FindWords(wordList);

            Response.Write(LongestWord[0] + "," + LongestWord[1]);
        }





        //public static List<string> FindWords(string[] list)
        //{
        //    var sortedWords = list.OrderByDescending(word => word.Length).ToList();
        //    var d = new List<string>(sortedWords);
        //    List<string> wordList = new List<string>();
        //    foreach (var word in sortedWords)
        //    {
        //        if (checkWords(word, d))
        //        {
        //            wordList.Add(word);
        //        }
        //    }
        //    return wordList;

        //}

        //private static bool checkWords(string word, List<string> d)
        //{
        //    if (String.IsNullOrEmpty(word)) return false;

        //    foreach (var part in splitWords(word))
        //    {
        //        if (d.Contains(part.Item1))
        //        {
        //            if (d.Contains(part.Item2))
        //            {
        //                return true;
        //            }
        //            else
        //            {
        //                return checkWords(part.Item2, d);
        //            }
        //        }
        //    }
        //    return false;
        //}

        //private static List<Tuple<string, string>> splitWords(string word)
        //{
        //    var splitWordList = new List<Tuple<string, string>>();
        //    for (int i = 1; i < word.Length; i++)
        //    {
        //        splitWordList.Add(Tuple.Create(word.Substring(0, i), word.Substring(i)));
        //    }
        //    return splitWordList;
        //}


        public static List<string> FindWords(string[] list)
    {
       var sortedWords = list.OrderByDescending(word => word.Length).ToList();
        var d = new HashSet<string>(sortedWords);
        List<string> wordList = new List<string>();
        foreach (var word in sortedWords)
        {
            if (isMadeOfWords(word, d))
            {  
                wordList.Add(word);             
            }
        }
        return wordList;
      
    }

      private static bool isMadeOfWords(string word, HashSet<string> d)
    {
        if (String.IsNullOrEmpty(word)) return false;
       
        foreach (var pair in generatePairs(word))
        {
            if (d.Contains(pair.Item1))
            {
                if (d.Contains(pair.Item2))
                {
                    return true;
                }
                else
                {
                    return isMadeOfWords(pair.Item2, d);
                }
            }
        }
        return false;
    }

     private static List<Tuple<string, string>> generatePairs(string word)
    
    {
        var output = new List<Tuple<string, string>>();
        for (int i = 1; i < word.Length; i++)
        {
            output.Add(Tuple.Create(word.Substring(0, i), word.Substring(i)));
        }
        return output;
    }



    }
}
