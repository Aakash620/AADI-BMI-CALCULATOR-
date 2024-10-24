# AADI-BMI-CALCULATOR-
import { useState } from 'react';
import { Input } from "/components/ui/input";
import { Label } from "/components/ui/label";
import { Button } from "/components/ui/button";
import { Card, CardContent, CardDescription, CardFooter, CardHeader, CardTitle } from "/components/ui/card";

const BMICalculator = () => {
  const [weight, setWeight] = useState('');
  const [height, setHeight] = useState('');
  const [bmi, setBmi] = useState('');
  const [category, setCategory] = useState('');

  const calculateBmi = () => {
    if (weight && height) {
      const bmiValue = Number(weight) / (Number(height) / 100) ** 2;
      setBmi(bmiValue.toFixed(2));
      if (bmiValue < 18.5) {
        setCategory('Underweight');
      } else if (bmiValue < 25) {
        setCategory('Normal weight');
      } else if (bmiValue < 30) {
        setCategory('Overweight');
      } else {
        setCategory('Obese');
      }
    }
  };

  return (
    <Card className="max-w-md mx-auto p-4">
      <CardHeader>
        <CardTitle>BMI Calculator</CardTitle>
        <CardDescription>Calculate your body mass index</CardDescription>
      </CardHeader>
      <CardContent>
        <div className="flex flex-col space-y-4">
          <div className="flex flex-col space-y-2">
            <Label htmlFor="weight">Weight (kg)</Label>
            <Input id="weight" type="number" value={weight} onChange={(e) => setWeight(e.target.value)} />
          </div>
          <div className="flex flex-col space-y-2">
            <Label htmlFor="height">Height (cm)</Label>
            <Input id="height" type="number" value={height} onChange={(e) => setHeight(e.target.value)} />
          </div>
        </div>
      </CardContent>
      <CardFooter>
        <Button onClick={calculateBmi}>Calculate BMI</Button>
        {bmi && (
          <div className="flex flex-col space-y-2 mt-4">
            <p>Your BMI is: {bmi}</p>
            <p>Category: {category}</p>
          </div>
        )}
      </CardFooter>
    </Card>
  );
};

export default BMICalculator;
