# LabReport4

## Code changes

![1](https://user-images.githubusercontent.com/97646229/165002636-50fb0860-f8ae-47d1-a812-cb663e346d48.png)
![2](https://user-images.githubusercontent.com/97646229/165002638-c8748769-8561-49a7-87f0-f1189c0aac5b.png)
![3](https://user-images.githubusercontent.com/97646229/165002640-0fa16f40-4a49-4f95-bd94-64b724942585.png)

## Failure inducing input

[Failure inducing input](https://github.com/Jojo4511/markdown-parser/blob/main/test-file.md)

## Symptom of failure inducing input

![image](https://user-images.githubusercontent.com/97646229/165002784-93b90445-af61-4459-bbd7-a86fa3fbafca.png)

## Relationship between the bug, the symptom, and failure inducing input

The failure inducing input is a line containing the format for a link without a closing parenthesis.
This causes a symptom where a StringIndexOutOfBoundsException is thrown due to a negative index attempting to be used.
This symptom is due to a bug in the code where the program cannot find the closing parenthesis because it is not given,
becuase of this a negative value is return for the position of the parenthesis and the program cannot end its substring operation at a negative index.
