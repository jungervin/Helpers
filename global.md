# Global Binding
```csharp
namespace WpfApp1
{
    public partial class App : Application
    {
        public static App Global = null;
        public App() : base()
        {
            App.Global = this;
            this.User = new User();
            this.User.Name = "Jung Ervin";
            this.User.Enabled = true;
        }

        private User FUser;

        public User User
        {
            get { return FUser; }
            set
            {
                FUser = value;
            }
        }
    }
}
```
In xaml:

```csharp
...
xmlns:local="clr-namespace:WpfApp1"
...
<TextBlock Text="{Binding Source={x:Static local:App.Global}, Path=User.Name}" />
```
