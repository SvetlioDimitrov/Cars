import json
import pandas as pd
import logging


class Cars:
    # init method to read the json file and to create the dataframe
    def __init__(self, filename='cars.json'):
        self.filename = filename
        self.records = []
        self.df = pd.read_json(filename)

    # function to load the data from the file

    def load_data(self):
        try:
            with open(self.filename) as cars_file:
                data = json.load(cars_file)
                self.records = data.get('data', [])
                print("JSON is valid.")
                logging.info("Json file is valid.")
        except json.JSONDecodeError as e:
            print("JSON is not valid:", e)
            logging.error("JSON is not valid")
        except FileNotFoundError:
            print("File not found.")
            logging.error("JSON is not valid")

    # function to find the number of unique cars

    def no_of_unique_cars(self):
        unique_cars = self.df['Name'].nunique()
        print("Number of unique cars: " + str(unique_cars))

    # function to find the average horsepower

    def average_horsepower(self):
        avg_hp = self.df['Horsepower'].mean()
        print("Average horsepower: " + str(avg_hp))

    # function to find the top 5 heaviest cars

    def heaviest_cars(self):
        heaviest_5 = self.df.nlargest(5, "Weight_in_lbs")
        print("Top 5 heaviest cars: \n" + str(heaviest_5))

    # function to find the number of cars by manufacturer

    def cars_by_manufacturer(self):
        self.df["Manufacturer"] = self.df.Name.str.split().str.get(0)

        cars_by_manufacturer = self.df.groupby("Manufacturer")["Name"].count()

        print("Number of cars by manufacturer: \n" + str(cars_by_manufacturer))

    # function to find the number of cars by year

    def cars_by_year(self):
        self.df['Year_made'] = pd.DatetimeIndex(self.df['Year']).year

        cars_by_year = self.df.groupby("Year_made")["Name"].count()

        print("Number of cars by year: \n" + str(cars_by_year))

    # function to save the data into csv file

    def save_file(self):
        self.df.to_csv('cars.csv', index=False)


c = Cars()
c.no_of_unique_cars()
c.average_horsepower()
c.heaviest_cars()
c.cars_by_manufacturer()
c.cars_by_year()
c.save_file()
