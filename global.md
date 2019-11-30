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
### xaml:

```csharp
...
xmlns:local="clr-namespace:WpfApp1"
...
<TextBlock Text="{Binding Source={x:Static local:App.Global}, Path=User.Name}" />
```

### user:
```csharp
public class User : INotifyPropertyChanged
    {

        private bool FEnabled = false;
        public bool Enabled
        {
            get { return FEnabled; }
            set
            {
                FEnabled = value;
                this.OnPropertyChanged();
            }
        }

        private String FName;

        public String Name
        {
            get { return FName; }
            set
            {
                FName = value;
                this.OnPropertyChanged();
            }
        }

        public event PropertyChangedEventHandler PropertyChanged;

        protected virtual void OnPropertyChanged([CallerMemberName] string propertyName = null)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
```
