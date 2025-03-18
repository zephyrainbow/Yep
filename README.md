## Code Listing
Rectangle
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Summative_8.Shapes
{
    internal class Rectangle : Shape
    {
        public const int MIN_HEIGHT = 0;
        public const int MAX_HEIGHT = 50;
        public const int MIN_WIDTH = 0;
        public const int MAX_WIDTH = 50;

        private float _Height;
        private float _Width;
        public float Height { get; set; }
        public float Width { get; set; }
        public Rectangle(float width, float height, Colour colour)
        {
            Width = width;
            Height = height;
            ShapeColour = colour;
        }

        public override float Area()
        {
            return _Height * _Width;
        }

        public override float Perimeter()
        {
            return 2 * _Width + 2 * _Height;
        }

        public override string ToString()
        {
            return $"{ShapeColour} Rectangle with height {Height} and width {Width}.";
        }
    }
}
```
AddRectangleMenuItem
```cs
using Summative_8.Shapes;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static Summative_8.Shapes.Shape;

namespace Summative_8.Menu
{
    internal class AddRectangleMenuItem : MenuItem
    {
        private ShapeManager _manager;

        public AddRectangleMenuItem(ShapeManager manager)
        {
            _manager = manager;
        }

        public override string MenuText()
        {
            return "Add rectangle menu";
        }

        public override void Select()
        {
            ColourShapeMenuItem selectColourMenu = new ColourShapeMenuItem();
            selectColourMenu.Select();
            Colour colour = selectColourMenu.Colour;
            int width = ConsoleHelpers.GetIntegerInRange(Rectangle.MIN_WIDTH, Rectangle.MAX_WIDTH, "What is the width");
            int height = ConsoleHelpers.GetIntegerInRange(Rectangle.MIN_HEIGHT, Rectangle.MAX_HEIGHT, "What is the height");
            Rectangle rectangle = new Rectangle(width, height, colour);
            _manager.AddShape(rectangle);
        }
    }
}

```
EditRectangleHeightMenuItem
```cs
using Summative_8.Shapes;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Summative_8.Menu
{
    internal class EditRectangleHeightMenuItem : MenuItem
    {
        private Rectangle _rectangle;

        public EditRectangleHeightMenuItem(Rectangle rectangle)
        {
            _rectangle = rectangle;
        }

        public override string MenuText()
        {
            return "Edit width";
        }

        public override void Select()
        {
            _rectangle.Height = ConsoleHelpers.GetIntegerInRange(Rectangle.MIN_HEIGHT, Rectangle.MAX_HEIGHT, "Enter new height");
        }
    }
}
```
EditRectangleHeightMenuItem
```cs
using Summative_8.Shapes;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Summative_8.Menu
{
    internal class EditRectangleWidthMenuItem : MenuItem
    {
        private Rectangle _rectangle;

        public EditRectangleWidthMenuItem(Rectangle rectangle)
        {
            _rectangle = rectangle;
        }

        public override string MenuText()
        {
            return "Edit width";
        }

        public override void Select()
        {
            _rectangle.Width = ConsoleHelpers.GetIntegerInRange(Rectangle.MIN_WIDTH, Rectangle.MAX_WIDTH, "Enter new width");
        }
    }
}
```

EditRectangleMenu
```cs
using Summative_8.Shapes;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Summative_8.Menu
{
    internal class EditRectangleMenu : EditShapeMenu
    {
        private Rectangle _rectangle;

        public EditRectangleMenu(Rectangle rectangle) : base(rectangle)
        {
            _rectangle = rectangle;
        }

        public override void CreateMenu()
        {
            base.CreateMenu();
            _menuItems.Add(new EditRectangleWidthMenuItem(_rectangle));
            _menuItems.Add(new EditRectangleHeightMenuItem(_rectangle));
            _menuItems.Add(new ExitMenuItem(this));
        }
    }
}
```
