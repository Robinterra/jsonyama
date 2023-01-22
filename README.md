Ein Yama Json Serializer

```csharp
namespace "Program"
{
    using "System";
    using "System.Text";
    using "System.IO";
    using "System.Runtime";
    using "System.Reflection";
    using "System.Collections";
    using "System.Runtime.IO";

    public class Tester
    {
        public String Text;
        public int Wisdom;

        public this new()
        {
            this.Wisdom = 0x42;

            return this;
        }

        public this ~()
        {

        }
    }


    public static class Program
    {

        static int main(Array array)
        {

            // Initialiserung einer Klasse zum Serialisieren
            Tester t = new Tester();
            t.Text = "hallo" + "Welt";

            TypeInfo typ = typeof<Tester>;

            // Serialisierung
            MemoryStream stream = new MemoryStream();
            &Stream s = (stream) as Stream;
            &object obj = (t) as object;
            JsonSerializer.Serialize(s, obj, typ);

            // Ausgabe in der Console
            RefString refs = stream.ToRefString();
            String result = refs.ToString();
            Console.PrintLine(result.Content);

            // Deserialiseriung
            RefString input = RefString.Pack(result.Content);
            TypeInfo type = typeof<Tester>;
            JsonDeserilaizeResponse te = JsonSerializer.DeSerialize(input, type);

            // Fehlerhanlding
            if (!te.IsSuccess)
            {
                Console.Print("(");
                Console.Print(te.Line);
                Console.Print(",");
                Console.Print(te.Column);
                Console.Print(") ");
                Console.PrintLine(te.Message);

                return 1;
            }

            Tester tt = (te.Result) as Tester;
            if (tt is null)
            {
                Console.Print("null");
                return 2;
            }

            &String ss = tt.Text;
            if (ss is null) return 1;
            Console.PrintLine(ss.Content);

            if (tt.Wisdom == 0x42) Console.PrintLine("yeeeaj");

            return 0;

        }

    }
}
```