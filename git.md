import java.io.IOException;

public class GitLabCommitAndPush {

    public static void main(String[] args) {
        String repositoryPath = "/path/to/your/local/repository";
        String filePath = "/path/to/your/file/to/commit";
        String commitMessage = "Your commit message";

        try {
            // Change to the repository directory
            ProcessBuilder changeDirBuilder = new ProcessBuilder("bash", "-c", "cd " + repositoryPath);
            Process changeDirProcess = changeDirBuilder.start();
            int changeDirExitCode = changeDirProcess.waitFor();

            if (changeDirExitCode != 0) {
                System.err.println("Error changing directory to the repository.");
                return;
            }

            // Add the file to the staging area
            ProcessBuilder addBuilder = new ProcessBuilder("git", "add", filePath);
            Process addProcess = addBuilder.start();
            int addExitCode = addProcess.waitFor();

            if (addExitCode != 0) {
                System.err.println("Error adding file to the staging area.");
                return;
            }

            // Commit the changes
            ProcessBuilder commitBuilder = new ProcessBuilder("git", "commit", "-m", commitMessage);
            Process commitProcess = commitBuilder.start();
            int commitExitCode = commitProcess.waitFor();

            if (commitExitCode != 0) {
                System.err.println("Error committing changes.");
                return;
            }

            // Push the changes to the remote repository
            ProcessBuilder pushBuilder = new ProcessBuilder("git", "push");
            Process pushProcess = pushBuilder.start();
            int pushExitCode = pushProcess.waitFor();

            if (pushExitCode != 0) {
                System.err.println("Error pushing changes to the remote repository.");
                return;
            }

            System.out.println("Changes committed and pushed successfully.");
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
