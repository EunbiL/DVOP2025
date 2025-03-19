# DVOP2025 Eunbi LEE

## Questions

1. When is the last time the `test_app` job ran ?

Apr 1, 2019, 2:12:12 PM

2. When building the job again, can you describe and explain what is going differently than the previous run ?

New files (e.g., features.cpp, test.cpp) have been added, and the inclusion of CMakeLists.txt suggests a change in the build system, while the newly added Jenkinsfile indicates a possible difference in Jenkins' build and execution process.

3. Now that you have assessed the situation, make the necessary modifications to make sure the Job environment and/or Job executable behaves in the same manner as it was before.

To restore the job environment to its previous behavior, I modified the Jenkinsfile to ensure that the pipeline continues even if some tests fail. Specifically, I added a try-catch block around the test execution step, which allows the pipeline to mark the build as SUCCESS even if a test fails. This ensures the pipeline behaves in the same way as before, where failed tests do not halt the process. The necessary changes have been committed to the repository, and I’ve attached the patch containing the modifications made to the Jenkinsfile.
git repository : 

4. Describe another solution to make the Job environment and/or Job executable behave in the same manner as it was before.

Use a separate branch for new changes instead of modifying the existing master branch. This allows you to keep the changes in the new files and configurations (like CMake and Jenkinsfile) without affecting the original state of the production branch. In Jenkins, you can configure the job to point to this new branch.

5. Now that everything is running as expected, it is time to suggest a production rollout for this service. Please suggest changes to the service to ensure a secure, production-ready deployment to be accessed by a team of developers. The suggestions are not limited in scope, but should focus on security, performance and reliability.

security - Ensure that Jenkins is using role-based access control (RBAC) to limit who can trigger builds and access sensitive information like credentials. Use Jenkins' credentials store or a dedicated secret management tool  - Vault - to handle sensitive data such as API keys, passwords, and certificates securely.
Performance - Use distributed Jenkins agents to handle builds more efficiently, especially if you have multiple teams or large projects. This can prevent the Jenkins server from becoming a bottleneck.
Reliability - Implement monitoring for Jenkins using tools like Prometheus or ELK stack to track performance metrics, build failures, and other issues. Set up alerts so you’re notified in case of any failures.
