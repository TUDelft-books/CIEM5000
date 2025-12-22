%```{margin}
%
%::::::{attention}
%This page shows the graded assignment. 
%
%Please open the assignment from [GitHub Classroom](https://classroom.github.com/a/NIabj19c) to work on it locally. The solution won't be provided.
%::::::
%
%```


# Graded assignment

%```{custom_download_link} https://classroom.github.com/a/NIabj19c
%:text: "GitHub Classroom repository"
%:replace_default: "False"
%```

When you've finished the workshops, you can start with the graded assignment. The process is very similar to the workshops, but now there's a deadline and you're required to write a report. You're going to solve the following model for displacements and internal forces using the Matrix Method.

%```{figure} figures/graded_assignment.svg
%```


First, analyse the model and the questions you're required to answer:
1. Explain what effect hinges have on the matrix method. The following questions might help you:
2. Explain in words and math how you adapted/added code and/or procedures to solve this structure.
3. Describe alternatives you considered for your implementation in the previous steps.
4. Make a table of all nodal displacement and show the displaced structure in a figure. Indicate how you identify nodes.
5. Show the moment diagram of the structure in a figure.
6. Provide a figure of a free body diagram of the full structure in which you show all the forces working on the structure (including support reactions) with numerical values from your code. This specific figure can be hand drawn.
7. Provide a figure of a free body diagram of the indicated node with numerical values from your code. This specific figure can be hand drawn. If you implement code for this in the matrixmethod package, make sure to perform sanity checks.
8. Comment on any potential mistakes you observed in your final answers.
9. If you had the time to expand this Matrix Method with an additional feature, what would that be?

Then, add potential new implementations to your code in `./matrixmethod/`. Please note that `./matrixmethod/` doesn't include any solutions from the workshops. If you've made new implementations, provide sanity checks to your implementations in `Graded_Implement.ipynb`. Then, solve and postprocess the problem in `Graded_Apply.ipynb`. Add a report in `.pdf` or `.md` format in which you included answers and reasoning for all the questions. Make sure all the values/figures you use in the report are solved/created with your code. Except for question 6 and 7: the free-body-diagrams can be hand-drawn. Furthermore, you're expected to provide to logically organise any auxiliary files you may use.

%he deadline of the assignment is April 19th, 23:59, although you’re encouraged to finish it directly after completing workshop 2. Doing so allows you to split the workload evenly. Commit and push all your files to the provided GitHub Classroom repository to hand in your assignment. Your latest commit before the deadline in the `main` branch will be graded. Incomplete assignments will be graded with a 1. The full solution won't be provided.

%You can take the resit of this assignment in Q4. If you choose to do so, you can improve your first submission by resubmitting to the same repository. The deadline of the resit is June 21th, 23:59. For more information, see [](./course_information.md).
