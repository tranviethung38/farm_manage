// See https://aka.ms/new-console-template for more information
/*
Team 2: Đỗ Gia Bảo + Nguyễn Minh Trí + Trần Việt Hùng
*/

namespace FarmManage 
{
    public class Animal
    {
        //Các field
        protected string sName;
        protected int iID;
        protected int iDate;
        protected int iMonth;
        protected int iYear; 
        protected int iNumOfAnimal;
        protected string sOrigin;
        protected string sPurpose;
        protected int iDateExport;
        protected int iMonthExport; 
        protected int iYearExport;     

        //Các properties
        public string Name
        {
            get { return this.sName; }
            set { this.sName = value; }
        }
        public int ID
        {
            get { return this.iID; }
            set { this.iID = value; }
        }
        public int Date
        {
            get { return this.iDate; }
            set
            {
                if (this.Month == 1 || this.Month == 3 || this.Month == 5 || this.Month == 7 || this.Month == 8 || this.Month == 10 || this.Month == 12)
                    if (value < 0 || value > 32)
                        throw new ArgumentOutOfRangeException(
                            $"{nameof(value)} must be between 0 and 31.");
                    this.iDate = value;
                
                if (this.Month == 4 || this.Month == 6 || this.Month == 9 || this.Month == 11)
                    if (value < 0 || value > 31)
                        throw new ArgumentOutOfRangeException(
                            $"{nameof(value)} must be between 0 and 30.");
                    this.iDate = value;
                if (this.Month == 2)
                    if (this.Year % 2 == 0)
                    {
                        if (value < 0 || value > 30)
                        throw new ArgumentOutOfRangeException(
                            $"{nameof(value)} must be between 0 and 29.");
                    this.iDate = value;
                    }
                    else
                    {
                        if (value < 0 || value > 29)
                        throw new ArgumentOutOfRangeException(
                            $"{nameof(value)} must be between 0 and 28.");
                    this.iDate = value;
                    }
            }
        }
        public int Month
        {
            get { return this.iMonth;}
            set
            {
            if (value < 0 || value > 13)
            throw new ArgumentOutOfRangeException(
            $"{nameof(value)} must be between 0 and 12.");
            this.iMonth = value;
            }
        }
        public int Year
        {
            get { return this.iYear; }
            set { this.iYear = value; }
        }
        public int NumOfAnimal
        {
            get { return this.iNumOfAnimal; }
            set { this.iNumOfAnimal = value; }
        }
        public string Origin
        {
            get { return this.sOrigin; }
            set { this.sOrigin = value; }
        }
        public string Purpose
        {
            get { return this.sPurpose; }
            set { this.sPurpose = value; }
        }
        public int DateExport 
        {
            get {return this.iDateExport;}
            set {this.iDateExport = value;}
        }
        public int MonthExport 
        {
            get {return this.iMonthExport;}
            set {this.iMonthExport = value;}
        }
        public int YearExport 
        {
            get {return this.iYearExport;}
            set {this.iYearExport = value;}
        }
        //Các constructors
        public Animal()
        {
        }
        public Animal(string name, int iD, int date, int month, int year, int numOfAnimal, string origin, string purpose)
        {
            this.Name = name;
            this.ID = iD;
            this.Date = date;
            this.Month = month;
            this.Year = year;
            this.NumOfAnimal = numOfAnimal;
            this.Origin = origin;
            this.Purpose = purpose;
        }
        public Animal(string name, string origin, string purpose)
        {
            this.Name = name;
             this.Origin = origin;
            this.Purpose = purpose;
        }
        public Animal(string name, string origin)
        {
            this.Name = name;
             this.Origin = origin;
        }
        public Animal(string name)
        {
            this.Name = name;
        }
    }
}
    class ManageAnimal:Animal
    {
        private List<Animal> ListAnimal = null;

        public ManageAnimal() {
            ListAnimal = new List<Animal>();
        }
        
        //Hàm tạo ID tăng dần cho đông vật 
        private int GenerateID()
        {
            int max = 1;
            if (ListAnimal != null && ListAnimal.Count > 0)
            {
                max = ListAnimal[0].ID;
                foreach (Animal an in ListAnimal)
                {
                    if (max < an.ID)
                    {
                        max = an.ID;
                    }
                }
                max++;
            }
            return max;
        }
        //Hàm đếm số động vật 
        public int NumberOfAnimal()
        {
            int Count = 0;
            if (ListAnimal != null)
            {
                Count = ListAnimal.Count;
            }
            return Count;
        }
        //Hàm tìm động vật theo ID
        public Animal FindByID(int ID)
        {
            Animal searchResult = null;
            if (ListAnimal != null && ListAnimal.Count > 0)
            {
                foreach (Animal an in ListAnimal)
                {
                    if (an.ID == ID)
                    {
                        searchResult = an;
                    }
                }
            }
            return searchResult;
        }
        //Hàm nhập một động vật mới 
        public void InputAnimal()
        {
            //Khởi tạo 1 giống vật nuôi mới 
            Animal an = new Animal();
            an.ID = GenerateID();
            Console.Write("Enter a new breed name: ");
            an.Name = Convert.ToString(Console.ReadLine());
            Console.Write("Enter the number of breed: ");
            an.NumOfAnimal = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter the month of month of entry into the barn: ");
            an.Month = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter the date of date of entry into the barn: ");
            an.Date = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter the year of year of entry into the barn: ");
            an.Year = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter the origin of livestock breeds: ");
            an.Origin = Convert.ToString(Console.ReadLine());
            Select(an);
            ListAnimal.Add(an);
        }

        //Cập nhật thông tin 1 giống vật nuôi theo ID có sẵn
        public void UpdateAnimal(int ID)
        {
            Animal an = FindByID(ID);
            Console.WriteLine("\nSelect the information you want to change : ");    
            Console.WriteLine("------------------------MENU------------------------");
            Console.WriteLine("|    1. Name                                       |");
            Console.WriteLine("|    2. Number of breed                            |");
            Console.WriteLine("|    3. Month                                      |");
            Console.WriteLine("|    4. Date                                       |");
            Console.WriteLine("|    5. Year                                       |");
            Console.WriteLine("|    6. Origin                                     |");
            Console.WriteLine("|    7. Purpose                                    |");
            Console.WriteLine("----------------------------------------------------");
            Console.Write("Enter options: ");
            int key = Convert.ToInt32(Console.ReadLine());
            if (an != null)
            {
                switch (key)
                {
                    case 1:
                    {
                        Console.Write("Enter a new breed name : ");   
                        string name = Convert.ToString(Console.ReadLine());
                        // Nếu không nhập gì thì không cập nhật tên
                        if (name != null && name.Length > 0)
                        {
                            an.Name = name;
                        }
                        break;
                    }
                    case 2:
                    {
                        Console.Write("Enter the number of breed : ");
                        int num = Convert.ToInt32(Console.ReadLine());
                        if (num != null)
                        {
                            an.NumOfAnimal = num;
                        }
                        break;
                    }
                    case 3:
                    {
                        Console.Write("Enter the month of month of entry into the barn : ");
                        int month = Convert.ToInt32(Console.ReadLine());
                        if (month != null)
                        {
                            an.Month = month;
                        }
                        break;
                    }
                    case 4:
                    {
                        Console.Write("Enter the date of date of entry into the barn : ");
                        int date = Convert.ToInt32(Console.ReadLine());
                        if (date != null)
                        {
                            an.Date = date;
                        }
                        break;
                    }
                    case 5:
                    {
                        Console.Write("Enter the date of date of entry into the barn : ");
                        int year = Convert.ToInt32(Console.ReadLine());
                        if (year != null)
                        {
                            an.Year = year;
                        }
                        break;
                    }
                    case 6:
                    {
                        Console.Write("Enter the origin of livestock breeds: ");
                        string origin = Convert.ToString(Console.ReadLine());
                        if (origin != null && origin.Length > 0)
                        {
                            an.Origin = origin;
                        }
                        break;
                    }
                    case 7:
                    {
                    Select(an);
                    break;
                    }
                    default:
                    {
                        Console.WriteLine("\nDoes not have this function!");
                        Console.WriteLine("\nSelect the function in the menu box.");
                        break;
                    }
                } 
            }
            else
            {
                Console.WriteLine("Does not exist this animal.", ID);
            }
            
        }
        //Hàm xóa một giống vật nuôi nào đó theo ID
        public bool DeleteById(int ID)
        {
            bool IsDeleted = false;
            // tìm kiếm sinh viên theo ID
            Animal an = FindByID(ID);
            if (an != null)
            {
                IsDeleted = ListAnimal.Remove(an);
            }
            return IsDeleted;
        }
        //Hàm hiển thị danh sách động vật ra màn hình 
        public void ShowAnimal(List<Animal> listAN)
        {
        Console.WriteLine("{0, -5} {1, -20} {2,-2} {3,-2} {4, -13} {5, -15} {6, 12} {7,20} {8,20}" , "ID", "Name", "Date", "Month", "Year", "Number of Animal", "Origin", "Flock Purpose", "Date Export");
        if (listAN != null && listAN.Count > 0)
            {
                foreach (Animal an in listAN)
                {
                    Console.WriteLine("{0, -5} {1, -20} {2,0} {3,0} {4,0} {5,0} {6, 0} {7, 15} {8, 22} {9,15} {10,18} {11,0} {12,0} {13,0} {14,0}", an.ID, an.Name, an.Date, "/", an.Month, "/", an.Year, an.NumOfAnimal, an.Origin, an.Purpose, an.DateExport, "/", an.MonthExport, "/", an.YearExport);
                }
            }
            Console.WriteLine();
        }
        //Hàm trả về danh sách động vật hiện tại 
        public List<Animal> getListAnimal()
        {
            return ListAnimal;
        }
        //Hàm xây dựng để chọn sản phẩm mong muốn
        private void Select(Animal an)
        {
            Console.WriteLine("\nSelect flock purpose: ");    
            Console.WriteLine("------------------------MENU------------------------");
            Console.WriteLine("|    1. Egg                                        |");
            Console.WriteLine("|    2. Meal                                       |");
            Console.WriteLine("----------------------------------------------------");
            Console.Write("Enter options: ");
            int key = Convert.ToInt32(Console.ReadLine());
            do {
            if (key == 1)
            {
                an.Purpose = "Egg";
                an.DateExport = an.Date;
                an.MonthExport = an.Month + 5;
                if (this.MonthExport > 12)
                {
                    an.MonthExport = an.MonthExport - 12;
                    an.YearExport = an.Year + 1;
                }
                an.YearExport = an.Year;
            }
            if (key == 2)
            {
                Purpose = "Meal";
                an.DateExport = an.Date;
                an.MonthExport = an.Month + 4;
                if (an.MonthExport > 12)
                {
                    an.MonthExport = an.MonthExport - 12;
                    an.YearExport = an.Year + 1;
                }
                an.YearExport = an.Year;
            }
            else Console.WriteLine("Please enter again");
            } while (key > 4 || key < 0);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            ManageAnimal manage = new ManageAnimal();
            while (true)
            {
                Console.WriteLine("\nAnimal Management Program C#");
                Console.WriteLine("*************************MENU**************************");
                Console.WriteLine("**  1. Add animals.                                  **");
                Console.WriteLine("**  2. Update animal informations by ID.             **");
                Console.WriteLine("**  3. Delete animal by ID.                          **");
                Console.WriteLine("**  4. Show list animals.                            **");
                Console.WriteLine("**  0. Exit                                          **");
                Console.WriteLine("*******************************************************");
                Console.Write("Enter options: ");
                int key = Convert.ToInt32(Console.ReadLine());
                switch (key)
                {
                    case 1:
                    {
                        Console.WriteLine("\n1. Add animals.");
                        manage.InputAnimal();
                        Console.WriteLine("\nAdd animals successfully !");
                        break;
                    }

                    case 2:
                    {
                        if (manage.NumberOfAnimal() > 0)
                        {
                            int id;
                            Console.WriteLine("\n2. Update animal informations by ID. ");
                            Console.Write("\nNhap ID: ");
                            id = Convert.ToInt32(Console.ReadLine());
                            manage.UpdateAnimal(id);
                        }
                        else
                        {
                            Console.WriteLine("\nList of empty animals!");
                        }
                        break;
                    }

                    case 3:
                    {
                    if (manage.NumberOfAnimal() > 0)
                        {
                            int id;
                            Console.WriteLine("\n3. Delete animal by ID.");
                            Console.Write("\nNhap ID: ");
                            id = Convert.ToInt32(Console.ReadLine());
                            if (manage.DeleteById(id))
                            {
                                Console.WriteLine("\nAnimal has id = {0} that has been removed.", id);
                            }
                        }
                        else
                        {
                            Console.WriteLine("\nList of empty animals!");
                        }
                        break;
                    }

                    case 4:
                    {
                        if (manage.NumberOfAnimal() > 0)
                        {
                            Console.WriteLine("\n4. Show list animals.");
                            manage.ShowAnimal(manage.getListAnimal());
                        }
                        else
                        {
                            Console.WriteLine("\nList of empty animals!");
                        }
                        break;
                    }

                    case 0:
                        Console.WriteLine("\nYou chose to exit the program!");
                        return;
                    default:
                    {
                        Console.WriteLine("\nDoes not have this function!");
                        Console.WriteLine("\nSelect the function in the menu box.");
                        break;
                    }
                }
            }
        }
    } 
