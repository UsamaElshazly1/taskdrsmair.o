# taskdrsmair.o
using System;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        int n = Convert.ToInt32(Console.ReadLine());
        int[] arr = new int[n];
        for (int i = 0; i < n; i++)
        {
            arr[i] = Convert.ToInt32(Console.ReadLine());
        }

        Array.Sort(arr);

        double median = 0;
        if (n % 2 == 0)
        {
            median = (arr[n / 2] + arr[n / 2 - 1]) / 2.0;
        }
        else
        {
            median = arr[n / 2];
        }

        var mode = arr.GroupBy(x => x).OrderByDescending(x => x.Count()).ThenBy(x => x.Key).First().Key;

        int range = arr.Max() - arr.Min();

        double firstQuartile = Quartile(arr, 0.25);
        double thirdQuartile = Quartile(arr, 0.75);

        double p90 = Percentile(arr, 90);

        double interquartileRange = thirdQuartile - firstQuartile;

        double lowerBound = firstQuartile - (1.5 * interquartileRange);
        double upperBound = thirdQuartile + (1.5 * interquartileRange);

        Console.WriteLine("Median: " + median);
        Console.WriteLine("Mode: " + mode);
        Console.WriteLine("Range: " + range);
        Console.WriteLine("First Quartile: " + firstQuartile);
        Console.WriteLine("Third Quartile: " + thirdQuartile);
        Console.WriteLine("P90: " + p90);
        Console.WriteLine("Interquartile Range: " + interquartileRange);
        Console.WriteLine("Outlier Boundaries: " + lowerBound + " - " + upperBound);
    }

    static double Quartile(int[] elements, double quart)
    {
        Array.Sort(elements);
        int index = (int)(quart * elements.Length);
        if (elements.Length % 2 == 0)
            return (elements[index] + elements[index - 1]) / 2.0;
        else
            return elements[index];
    }

    static double Percentile(int[] elements, int percentile)
    {
        Array.Sort(elements);
        int index = (int)Math.Ceiling((percentile / 100.0) * elements.Length) - 1;
        return elements[index];
    }
}
```
