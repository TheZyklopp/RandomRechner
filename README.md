# RandomRechner
````csharp
using System.ComponentModel.Design;
using System.Numerics;

namespace RandomRechner
{
    internal class Program
    {
        static void Main(string[] args)
        {
            //schleife zum ablaufen so oft wie man rechnen m�chte.
            bool erneut = true;
            while (erneut == true)
            {
                //leitet weiter und rechnet Zufallzahl.
                int a = Zufall();
                int b = Zufall();

                //rechnet a*b
                int losung = Calculate(a, b);

                //schleife f�r die eigene rechnung.
                bool stimmt = false;
                while (stimmt == false)
                {
                    Console.WriteLine($"Was ist {a} * {b}");

                    string prufen = Console.ReadLine();
                    //pr�ft ob die eingabe eine Zahl ist.
                    int eingabe = IstZahl(prufen);

                    //Pr�ft ob die eingabe stimmt oder nicht.
                    stimmt = Prufen(losung, eingabe);

                }
                Console.WriteLine("Nochmal? Y / N");
                //�berpr�ft ob man weiter spielen will mit der eingabe Y N
                char key = YesOrNo();

                if (key == 'Y')
                {
                    erneut = true;
                }
                else{
                    erneut = false;
                }

            }
        }

        //pr�ft ob eingabe eine Zahl ist.
        static int IstZahl(string eingabe)
        {

            int zahl;

            while (true)
            {
                if (int.TryParse(eingabe, out zahl))
                {
                    return zahl;
                }
                else
                {
                    Console.WriteLine("Dies ist keine Zahl.");
                    eingabe = Console.ReadLine();
                }
            }
        }


        static int Zufall()
        {
            //gibt eine Zahl von 1-100 wieder
            Random rnd = new Random();
            int zufallzahl = rnd.Next(1, 100);

            return zufallzahl;
        }

        static int Calculate(int zahl1, int zahl2)
        {
            //rechnet zusammen a und b
            return (zahl1 * zahl2);
        }

        //pr�ft ob eingabe richtig ist.
        static bool Prufen(int losung, int eingabe)
        {           
            while (true)
            {
                if (losung == eingabe)
                {
                    Console.WriteLine($"Richtig die L�sung ist {losung}");
                    return true;
                }
                else
                {
                    Console.WriteLine($"Falsch");
                    return false;
                }
            }
        }

        //weiterspielen?
        static char YesOrNo()
        {
            while (true)
            {
                ConsoleKeyInfo key = Console.ReadKey(intercept: true);
                char eingabe = char.ToUpper(key.KeyChar);

                if (eingabe == 'Y' || eingabe == 'N')
                {
                    Console.WriteLine(eingabe);
                    return eingabe;
                }
                else
                {
                    Console.WriteLine("\nUng�ltige Eingabe. Bitte 'y' oder 'n' dr�cken.");
                }
            }
        }
    }
}
