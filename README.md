# git-release

Create a release from an arbitrary git repository.

## Usage

Create a `.version` file at the top of your repository. The version must be semantic versioning version number, optionally followed by `-SNAPSHOT`. Next, simply run:

```console
$ git-release --repository-path=...
```

Example output:

```console
Working in /Users/rad/dev/golang/src/github.com/radekg/terraform-provisioner-ansible/
go test -v ./...
=== RUN   TestResourceProvisioner_impl
--- PASS: TestResourceProvisioner_impl (0.00s)
=== RUN   TestProvisioner
--- PASS: TestProvisioner (0.00s)
=== RUN   TestBadConfig
--- PASS: TestBadConfig (0.00s)
=== RUN   TestGoodAndCompleteRemoteConfig
--- PASS: TestGoodAndCompleteRemoteConfig (0.00s)
=== RUN   TestGoodLocalConfigWithoutPlaybookWarnings
--- PASS: TestGoodLocalConfigWithoutPlaybookWarnings (0.00s)
=== RUN   TestRequirePlaybookFilePath
--- PASS: TestRequirePlaybookFilePath (0.00s)
=== RUN   TestRequireModuleName
--- PASS: TestRequireModuleName (0.00s)
=== RUN   TestConfigWithoutPlaysFails
--- PASS: TestConfigWithoutPlaysFails (0.00s)
=== RUN   TestConfigWithPlaysbookAndModuleFails
--- PASS: TestConfigWithPlaysbookAndModuleFails (0.00s)
=== RUN   TestConfigWithInvalidValueTypeFailes
--- PASS: TestConfigWithInvalidValueTypeFailes (0.00s)
=== RUN   TestConfigProvisionerParserDecoder
--- PASS: TestConfigProvisionerParserDecoder (0.00s)
PASS
ok  	github.com/radekg/terraform-provisioner-ansible	(cached)
=== RUN   TestLocalInventoryTemplateGeneratesWithAlias
--- PASS: TestLocalInventoryTemplateGeneratesWithAlias (0.00s)
=== RUN   TestLocalInventoryTemplateGeneratesWithoutAlias
--- PASS: TestLocalInventoryTemplateGeneratesWithoutAlias (0.00s)
=== RUN   TestRemoteInventTemplateGenerates
--- PASS: TestRemoteInventTemplateGenerates (0.00s)
PASS
ok  	github.com/radekg/terraform-provisioner-ansible/mode	(cached)
?   	github.com/radekg/terraform-provisioner-ansible/types	[no test files]
- branch is master.
- master is up to date with origin/master

Release version [2.0.2]:
2.1.0
Next version [2.1.1-SNAPSHOT]:


Write changes to remote repository and create the release (y/n)? [y]:

creating release 2.1.0...
[master d196a50] Release 2.1.0
 1 file changed, 1 insertion(+), 1 deletion(-)
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 260 bytes | 260.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:radekg/terraform-provisioner-ansible.git
   6fa0f9c..d196a50  master -> master
Total 0 (delta 0), reused 0 (delta 0)
To github.com:radekg/terraform-provisioner-ansible.git
 * [new tag]         v2.1.0 -> v2.1.0
[master 7558797] Update version to 2.1.1-SNAPSHOT
 1 file changed, 1 insertion(+), 1 deletion(-)
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 292 bytes | 292.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:radekg/terraform-provisioner-ansible.git
   d196a50..7558797  master -> master
Done \o/.
```

## Executing pre-release and post-release tasks

If the target repository contains an executable file called `git-release-before.sh`, this file will be executed before creating the release.

If the target repository contains and executable called `git-release-after.sh`, this file will be executed after the release has been created.

The programs can be overriden using:

- `--execute-before-release=...`: if program name is given, `$repository-path/$execute-before-release` will be used, if full path is given, that path will be executed, `~` is not expanded, use `$HOME` instead
- `--execute-after-release=...`: if program name is given, `$repository-path/$execute-after-release` will be used, if full path is given, that path will be executed, `~` is not expanded, use `$HOME` instead
