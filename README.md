# farm_manage
/*
Team 2: Đỗ Gia Bảo + Nguyễn Minh Trí + Trần Việt Hùng
*/

namespace FarmManage 
{
    public interface IDataImporter
    {
        void ImportData(string filePath);
    }
    public interface IDataExporter
    {
        void ExportDataAsTable();
        void ExportDataToFile(string filePath);
    }
    class Inform
    {
        //Các field
        private static int currentID;
       protected string sName {get;set;}
       protected int iID {get;}
       protected string sDate {get; set;}
       protected int iNumOfAnimal {get; set;}  

        public Inform()
        {
            sName = "Cow";
            iID = 0;
            sDate = "1/1/2021";
            iNumOfAnimal = 10;
        }
        public Inform (string name, string date, int numOfAnimal)
        {
            this.sName = name;
            this.iID = GetNextID();
            this.sDate = date;
            this.iNumOfAnimal = numOfAnimal;
        }
