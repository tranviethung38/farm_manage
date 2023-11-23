// See https://aka.ms/new-console-template for more information
/*
Team 2: Đỗ Gia Bảo + Nguyễn Minh Trí + Trần Việt Hùng
*/

namespace FarmManage 
{
    public class Animal
    {
        //Các field
        public string Name { get;set; }
        public int ID { get; set; }
        public string Date { get; set; }
        public int NumOfAnimal { get; set; }
       
    }
}
/*
Team 2: Đỗ Gia Bảo + Nguyễn Minh Trí + Trần Việt Hùng
*/
using System;
using System.Collections.Generic;

namespace FarmManage 
{
    class ManageAnimal
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
            Console.Write("Enter a new breed name : ");
            an.Name = Convert.ToString(Console.ReadLine());
            Console.Write("Enter the number of breed : ");
            an.NumOfAnimal = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter the date of date of entry into the barn : ");
            an.Date = Convert.ToString(Console.ReadLine());
            ListAnimal.Add(an);
        }
        //Cập nhật thông tin 1 giống vật nuôi theo ID có sẵn
        public void UpdateAnimal(int ID)
        {
            Animal an = FindByID(ID);
            if (an != null)
            {
                Console.Write("Enter a new breed name : ");   
                string name = Convert.ToString(Console.ReadLine());
                // Nếu không nhập gì thì không cập nhật tên
                if (name != null && name.Length > 0)
                {
                    an.Name = name;
                }
                Console.Write("Enter the number of breed : ");
                int num = Convert.ToInt32(Console.ReadLine());
                if (num != null)
                {
                    an.NumOfAnimal = num;
                }
                Console.Write("Enter the date of date of entry into the barn : ");
                string date = Convert.ToString(Console.ReadLine());
                if (date != null && date.Length > 0)
                {
                    an.Date = date;
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
        Console.WriteLine("{0, -5} {1, -20} {2, -5} {3, 5}", "ID", "Name", "Date", "Number of Animal");
        if (listAN != null && listAN.Count > 0)
            {
                foreach (Animal an in listAN)
                {
                    Console.WriteLine("{0, -5} {1, -20} {2, -5} {3, 5}", an.ID, an.Name, an.Date, an.NumOfAnimal);
                }
            }
            Console.WriteLine();
        }
        //Hàm trả về danh sách động vật hiện tại 
        public List<Animal> getListAnimal()
        {
            return ListAnimal;
        }
    }
}
// See https://aka.ms/new-console-template for more information
/*
Team 2: Đỗ Gia Bảo + Nguyễn Minh Trí + Trần Việt Hùng
*/

namespace FarmManage 
{
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
                Console.Write("Nhap tuy chon: ");
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
                            Console.WriteLine("\n2. Cap nhat thong tin sinh vien. ");
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
                        Console.WriteLine("\nDoes not have this function!");
                        Console.WriteLine("\nSelect the function in the menu box.");
                        break;
                }
            }
        }
    } 
}
