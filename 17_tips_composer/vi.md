#  Composer

## 17+ lời khuyên để sử dụng composer hiệu quả

2018-01-05

Mặc dù hầu hết các dev PHP đều biết cách sử dụng Composer, nhưng không phải ai cũng sử dụng nó hiệu quả hoặc theo một cách tốt nhất có thể. Vì vậy, tôi quyết định tóm tắt những điều quan trọng trong quy trình làm việc hằng ngày của tôi.
Quan điểm chung của hầu hết các lời khuyên là _"Tránh rủi ro"_, điều đó có nghĩa là nếu có nhiều cách để xử lý một việc gì đó, tôi sẽ sử dụng cách tiếp cận ít lỗi nhất. 

## Lời khuyên #1: Đọc tài liệu

Tôi thực sự có ý đó. [Tài liệu](https://getcomposer.org/doc/) rất tuyệt và một vài giờ đọc nó sẽ giúp bạn tiết kiệm thời gian hơn trong thời gian dài. Bạn sẽ ngạc nhiên khi có bao nhiêu thứ mà Composer có thể làm được.

## Lời khuyên #2: Hãy nhận biết sự khác biế giữa "project" và "library"


Điều quan trọng nhất cần phải biết là bạn đang tạo ra một _"project"_ hay một _"library"_. Mỗi loại sẽ yêu cầu các bài thực hành riêng biệt.

Một library (thư viện) là một package có thể tái sử dụng, bạn nên thêm nó như là một `dependency`(phụ thuộc) - như là `symfony/symfony`, `doctrine/orm` hay [`elasticsearch/elasticsearch`](https://github.com/elastic/elasticsearch-php).

Một project (dự án) thường là một ứng dụng, phụ thuộc vào một vài thư viện. Nó thường không được tái sử dụng (những project khác không yêu cầu nó như là một phụ thuộc). Ví dụ điển hình như là các trang web thương mại điện tử, hệ thống hỗ trợ khách hàng, v.v..

Tôi sẽ phân biệt thư viện và dự án trong những lời khuyên bên dưới.

## Lời khuyên #3: Sử dụng các phiên bản phụ thuộc cụ thể cho các ứng dụng.

Nếu bạn đang tạo một ứng dụng, bạn nên sử dụng phiên bản cụ thể nhất để định nghĩa các phụ thuộc. Nếu bạn cần phân tích cú pháp các tệp YAML, bạn nên chỉ rõ sự phụ thuộc như sau `"symfony/yaml": "4.0.2"`.

Ngay cả khi thư viện tuân theo [Semantic Versioning](https://semver.org/), có thể có sự phá vỡ backwards-compatibility (khả năng tương thích ngược) trong các phiên bản nhỏ và bản vá. Ví dụ, nếu bạn đang sử dụng `"symfony/symfony": "^3.1"`, có thể có một số sự khác biệt trong bản 3.2, có thể làm phá vỡ bản test ứng dụng của bạn. Hoặc có thể sửa lỗi trong PHP_CodeSniffer và nó sẽ giúp phát hiện các vấn đề định dạng mới trong code của bạn, điều đó một lần nữa dẫn đến hỏng bản xây dựng code.  

Việc cập nhật các phụ thuộc nên được cân nhắc, không phải ngẫu nhiên. Một trong những lời khuyên bên dưới sẽ thảo luận chi tiết hơn.

Nghe có vẻ là quá mức cần thiết, nhưng điều này sẽ ngăn cho việc đồng nghiệp của bạn vô tình cập nhật tất cả các phụ thuộc khi thêm một thư viện mới vào trong dự án. (điều mà bạn có thể bỏ lỡ trong khi Code Review)

## Lời khuyên #4: Sử dụng phạm vi phiên bản cho các phụ thuộc thư viện. 

Nếu bạn đang tạo một thư viện, bạn nên xác định phạm vi phiên bản rộng nhất khả thi. Nếu bạn tạo một thư viện mà sử dụng thư viện `symfony/yaml` để phân tích cú pháp YAML, bạn nên yêu cầu nó như sau:

    
    
    "symfony/yaml": "^3.0 || ^4.0"
    

Điều đó có nghĩa là thư viện của bạn có thể sử dụng `symfony/yaml` với bất kì phiên bản Symfony 3.x hoặc  phiên bản 4.x. Nó rất quan trọng, bởi vì những hạn chế này sẽ được chuyển đến ứng dụng sử dụng thư viện của bạn.

Trong trường hợp có 2 thư viện có yêu cầu xung đột nhau, ví dụ một cái yêu cầu `~3.1.0` và cái khác yêu cầu `~3.2.0`, thì quá trình cài đặt sẽ thất bại.

## Lời khuyên #5: Bạn nên commit `composer.lock` lên git trong các ứng dụng

Nếu bạn đang tạo _một dự án_, bạn chắc chắn muốn commit `composer.lock` lên git. Điều này đảm bảo tất cả mọi người - bạn, đồng nghiệp của bạn, server CI của bạn và server production của bạn - đang chạy ứng dụng với các phiên bản phụ thuộc giống nhau.

Thoạt nhìn, nó nghe có vẻ không cần thiết - bạn đang sử dụng một phiên bản cụ thể trong những ràng buộc, như đã đề cập trong lời khuyên #3. Nhưng không, cũng có những phụ thuộc trong những phụ thuộc của bạn mà không bị hạn chế bởi những ràng buộc này (ví dụ `symfony/console` phụ thuộc vào `symfony/polyfill-mbstring`). Vì vậy, nếu không commit file `composer.lock`, bạn sẽ không lấy được một tập hợp các phụ thuộc giống nhau.

## Lời khuyên #6: Đặt `composer.lock` trong `.gitignore` ở các thư viện

Nếu bạn đang tạo _một thư viện_ (hãy gọi nó là `acme/my-library`), bạn không nên commit file `composer.lock`. Nó [không có tác dụng](https://getcomposer.org/doc/02-libraries.md#lock-file) trong các project đang sử dụng thư viện của bạn. Hãy tưởng tượng rằng `acme/my-library` sử dụng `monolog/monolog` như một sự phụ thuộc. Nếu bạn đã commit một file `composer.lock`, mọi người đang phát triển `acme/my-library` sẽ sử dụng một phiên bản cũ hơn của Monolog. Nhưng khi thư viện hoàn thành, và bạn sử dụng nó trong các project thật, một phiên bản mới hơn của Monolog có thể đã được cài đặt, và nó có thể  không tương thích với thư viện nữa. Nhưng bạn lại không chú ý đến điều đó trước, bởi vì `composer.lock`!

Điều đó sẽ tốt hơn khi đặt `composer.lock` trong file `.gitignore` của bạn để không vô tình commit nó.

Nếu bạn muốn đảm bảo rằng thư viện của bạn tương thích với các phiên bản khác nhau của các phụ thuộc, đọc tiếp các lời khuyên.

## Lời khuyên #7: Chạy Travis CI được xây dựng với các phiên bản phụ thuộc khác nhau
> Lời khuyên này chỉ áp dụng cho các thư viện (bởi vì bạn sử dụng các phiên bản cụ thể cho các ứng dụng)

Nếu bạn đang xây dựng một thư viện mã nguồn mở, bạn chắc hẳn đang sử dụng Travis CI để chạy các bản xây dựng của nó.

Theo mặc định, Composer cài đặt các phiên bản mới nhất có thể của các phụ thuộc được ràng buộc trong `composer.json`. Điều này có nghĩa là đối với các ràng buộc phụ thuộc `^3.0 || ^4.0`, bản xây dựng luôn được sử dụng phiên bản mới nhất của bản phát hành v4. Vì phiên bản 3.0 chưa bao giờ được kiểm tra, thư viện có thể không tương thích với nó và điều đó có thể làm cho người dùng của bạn cảm thấy không vui. 

May mắn thay, Composer cung cấp một bộ chuyển đổi để cài đặt các phiên bản thấp nhất có thể của phụ thuộc `--prefer-lowest` (nên sử dụng `--prefer-stable` để tránh việc cài đặt các phiên bản không ổn định)

Cấu hình `.travis.yml` được cập nhật có thể được thấy như sau:

    
    
    language: php
    
    php:
      - 7.1
      - 7.2
    
    env:
      matrix:
        - PREFER_LOWEST="--prefer-lowest --prefer-stable"
        - PREFER_LOWEST=""
    
    before_script:
      - composer update $PREFER_LOWEST
    
    script:
      - composer ci
    

Xem trực tiếp trong [thư viện mhujer/fio-api-php của tôi](https://github.com/mhujer/fio-api-php/blob/master/.travis.yml) và [ma trận xây dựng trên Travis CI](https://travis-ci.org/mhujer/fio-api-php)

Mặc dù giải pháp này có thể khắc phục được hầu hết các vấn đề không tương thích, nhưng nhớ rằng có nhiều sự kết hợp của các phụ thuộc giữa phiên bản thấp nhất và mới nhất. Và chúng có thể không tương thích với nhau. 

## Lời khuyên #8: Sắp xếp các packages trong require và require-dev theo tên.

Một cách thực hành tốt là sắp xếp các packages trong `require` và `require-dev` theo tên. Điều này có thể ngăn chặn các xung đột merge khi rabasing một nhánh. Bởi vì nếu bạn đã thêm một package vào cuối danh sách trong 2 branch, sẽ luôn có xung đột khi merge.

Đó là một công việc tẻ nhạt để làm thủ công, vì vậy cách tốt nhất là [cấu hình nó](https://getcomposer.org/doc/06-config.md#sort-packages trong `composer.json`:

    
    
    {
    ...
        "config": {
            "sort-packages": true
        },
    â¦
    }
    

Lần tới, bạn `require` một packages mới, nó sẽ được thêm vào vị trí thích hợp (và không phải ở cuối).

## Lời khuyên #9: Đừng merge `composer.lock` khi đang rebasing hoặc merging

Nếu bạn thêm một phụ thuộc mới vào `composer.json` (và `composer.lock`) và trước khi bạn merge nhánh của bạn, có một phụ thuộc đã được thêm vào master, bạn cần phải rebase nhánh của bạn. và bạn sẽ sẽ nhận được một merge-conflict trong `composer.lock`.

Bạn không bao giờ nên cố gắng giải quyết xung đột này theo cách thủ công, bởi vì file`composer.lock` có chứa một hàm băm của các phụ thuộc được định nghĩa trong `composer.json`. Vì vậy, ngay cả khi bạn giải quyết xung đột, kết quả file lock vẫn sẽ không chính xác.

Điều tốt nhất cần làm là tạo ra `.gitattributes` trong thư mục gốc của project với dòng sau, để thể hiện rằng git sẽ không bao giờ gộp `composer.lock`:

    
    
    /composer.lock -merge
    

Bạn có thể khắc phục vấn đề này bằng các sử dụng các nhánh tính năng ngắn hạn được gợi ý trong [Trunk Based Development](https://trunkbaseddevelopment.com/) (bạn nên thực hiện điều này). Khi bạn có một nhánh ngắn hạn, nó sẽ được gộp kịp thời, nguy cở xảy ra xung đột merge trong `composer.lock` là tối thiểu. Bạn thậm chí có thể tạo một branch để thêm một sự phụ thuộc và merge nó ngay lập tức.

Nhưng phải làm gì, nếu bạn gặp phải một xung đột merge trong `composer.lock` khi rebasing? giải quyết nó với phiên bản từ master, vì vậy bạn sẽ chỉ có thể thay đổi trong `composer.json` (package được thêm vào). và sau đó chạy `composer update --lock`, sẽ cập nhật file `composer.lock` với những thay đổi từ `composer.json`. Bây giờ bạn có thể cập nhật stage `composer.lock` và tiếp tục rabase

## Lời khuyên #10: Biết được sự khác nhau giữa `require` và `require-dev`

Điều quan trọng là nhận thức được sử khác nhau giữa khối `require` và `require-dev`.

Các package được required để chạy ứng dụng or thư viện nên được định nghĩa trong `require` (ví dụ Symfony, Doctrine, Twig, Guzzle, ...). Nếu bạn đang tạo ra một thư viện, hãy cẩn trọng những gì bạn đặt trong `require`. Bởi vì mỗi phụ thuộc trong phần này cũng là phụ thuộc trong ứng dụng, mà bạn sử dụng trong thư viện.

Các package cần thiết để phát triển ứng dụng (hoặc thư viện) nên được định nghĩa trong `require-dev` (ví dụ PHPUnit, PHP_CodeSniffer, PHPStan).

## Lời khuyên #11: Cập nhật các phụ thuộc 1 cách an toàn

T đoán rằng chúng ta đều có thể đồng ý 1 sự thật rằng các phụ thuộc nên được cập nhật một cách thường xuyên. vấn đề tôi muốn bàn ở đây là việc cập nhật các phụ thuộc nên được thực hiện một cách rõ ràng và cẩn trọng, chứ không phải chỉ cần làm cho xong như những công việc khác. Nếu bạn đang muốn sửa đổi một cái gì đó và cập nhật một vài thời điểm tại cùng thời điểm, bạn không thể dễ dàng biết rằng liệu ứng dụng đã bị hỏng do bạn sữa đổi hay do việc cập nhật đã gây nên.

Bạn có thể sử dụng câu lệnh `composer outdated` để xem các phụ thuộc nào có thể được cập nhật. Bạn có thêm lựa chọn `--direct` (hoặc `-D`) để chỉ hiện thị danh sách các phụ thuộc được khai báo trong `composer.json`. Ngoài ra còn có một lựa chọn `-m` chỉ để hiển thị các bản cập nhật ở mức nhỏ.

**Với mỗi phụ thuộc quá hạn thì thực hiện các bước sau đây:**:

  1. Tạo một nhánh mới
  2. Cập nhật phiên bản phụ thuộc trong `composer.json` đến một phiên bản mới nhất
  3. Chạy `composer update phpunit/phpunit --with-dependencies` (thay `phpunit/phpunit`bằng thư viện bạn đang cập nhật)
  4. Kiểm tra CHANGELOG trong kho lưu trữ thư viện trên Github để xem có bất kì thay đổi nào không. Nếu có hãy cập nhật ứng dụng.
  5. Kiểm tra ứng dụng cục bộ (Nếu bạn đang sử dụng Symfony, bạn có thể thấy cảnh báo lỗi trong Debug Bar).
  6. Commit các thay đổi (`composer.json`, `composer.lock` và những gì bạn thấy cần thiết cho phiên bản mới để làm việc)
  7. Đợi CI xây dựng xong.
  8. Merge and deploy

Đôi khi nó có ý nghĩa cập nhật phụ thuộc nhiều hơn cùng một lúc, ví dụ khi bạn đang cập nhật Doctrine hoặc Sysfony.  Trường hợp này bạn có thể liệt kê tất cả trong câu lệnh update:

    
    
    composer update symfony/symfony symfony/monolog-bundle --with-dependencies
    

Hoặc bạn có thể sử dụng wildcard để cập nhật tất cả phụ thuộc theo một namespace cụ thể:


    
    
    composer update symfony/* --with-dependencies
    

Tôi biết rằng tất cả những điều này nghe có vẻ thừa thãi, nhưng bạn chắc chắn sẽ cập nhật các phụ thuộc một các tình cờ, vì vậy sẽ an toàn hơn.

Một cách ngắn gọn là cập nhật tất cả các `require-dev` phụ thuộc cùng một lúc (nếu chúng không yêu cầu thay đổi code, nếu không tôi sẽ đề xuất sử dụng branch khác nhau để review code dễ dàng hơn)


## Lời khuyên #12: Bạn có thể định nghĩa các kiểu phụ thuộc khác `composer.json`

Ngoài việc định nghĩa thư viện như là các phụ thuộc, bạn cũng có thể định nghĩa những thứ khác ở đó.

Bạn có định nghĩa các thư viện PHP mà ứng dụng/thư viện của bạn hỗ trợ:

    
    
    "require": {
        "php": "7.1.* || 7.2.*",
    },
    

Bạn cũng có thể định nghĩa các phần mở rộng nào được yêu cầu cho ứng dụng/thư viện.
Điều này vô cùng hữu ích khi bạn cố gắng dockerize ứng dụng của bạn hay đồng nghiệp mới của bạn khi bạn cài đặt ứng dụng lần đầu tiên.

    
    
    "require": {
        "ext-mbstring": "*",
        "ext-pdo_mysql": "*",
    },
    

(Bạn nên sử dụng `*` cho phiên bản tiện ích mở rộng vì [chúng có thể không nhất quán](https://getcomposer.org/doc/01-basic-usage.md#platform-packages)).

## Lời khuyên #13: Xác thực `composer.json` trong quá trình xây dựng CI.

`composer.json` và `composer.lock` phải luôn giữ được đồng bộ. Do đó,
bạn có thể tự động kiểm tra điều này. Chỉ cần thêm điều này như là một phần đoạn mã khi bạn xây dựng script và nó đảm bảo `composer.lock` đồng bộ với `composer.json`:

    
    
    composer validate --no-check-all --strict
    

## Lời khuyên #14: Sử dụng plugin Composer trong PHPStorm

Có một  [plugin composer.json cho PHPStorm](https://plugins.jetbrains.com/plugin/7631-php-composer-json-support). Nó thêm bộ tự động hoàn thiện và xác thực khi thay đổi `composer.json` thủ công.

Nếu bạn đang sử dụng IDE khác (hoặc chỉ là một trình soạn thảo code), bạn có thể thiết lập xác thực đối với [JSON schema](https://getcomposer.org/schema.json).

## Lời khuyên #15: Chỉ định phiên bản production PHP trong `composer.json`

Nếu bạn giống như tôi và đôi khi bạn đang[chạy các phiên bản pre-released PHP trên local ](https://blog.martinhujer.cz/php-7-2-is-due-in-november-whats-new/), bạn đang có vấn đề trong việc cập nhật các phụ thuộc lên một phiên bản không hoạt đông trong production. Ngay bây giờ, tôi đang sử dụng PHP 7.2.0, có nghĩa là tôi có thể cài đặt thư viện, mà sẽ không hoạt động trên 7.1. production đang chạy trên 7.1, do đó việc cài đặt sẽ thất bại

Nhưng không cần phải lo lắng, có một cách dễ dàng. Chỉ cần chỉ định phiên bản production PHP trong `config` của `composer.json`:
    
    
    "config": {
        "platform": {
            "php": "7.1"
        }
    }
    

Đừng nhầm nó với phần `require`, nó hoàn toàn khác nhau. Ứng dụng của bạn có thể chạy trên 7.1 hoặc 7.2 và đồng thời chỉ định 7.1 làm nền tảng (có nghĩa là các phụ thuộc sẽ luôn được cập nhật lên phiên bản tương thích với phiên bản 7.1):
    
    
    "require": {
        "php": "7.1.* || 7.2.*"
    },
    "config": {
        "platform": {
            "php": "7.1"
        }
    },
    

## Lời khuyên #16: Sử dụng các packages cá nhân từ self-hosted Gitlab

Lời khuyên ở đây là sử dụng `vcs` như một loại repository và Composer sẽ tìm ra cách đúng để lấy các package phù hợp. Ví dụ nếu bạn đang thêm một fork từ Github, nó sẽ sử dụng API của nó để tải tệp xuống file zip thay vì clone toàn bộ repository.

Nhưng nó lại phức tạp hơn cho một cài đặt cá nhân trên Gitlab. Nếu bạn sử dụng `vcs` như một loại repository, Composer sẽ phát hiện ra rằng đây là một cài đặt Gitlab đang cố tải xuống package sử dụng API (yêu cầu API key)tôi không muốn thiết lập nó, vì vậy tôi đã cài đặt cho thiết lập này(sử dụng SSH  để clone):


Đầu tiên chỉ định repository với kiểu `git`:

    
    
    "repositories": [
        {
            "type": "git",
            "url": "git@gitlab.mycompany.cz:package-namespace/package-name.git"
        }
    ]
    

Sau đó sử dụng package mà bình thường bạn sẽ có:

    
    
    "require": {
        "package-namespace/package-name": "1.0.0"
    }
    

## Lời khuyên #17: Làm thế nào để tạm thời sử dụng một branch với bugfix từ fork

Nếu như bạn tìm một lỗi trong thư viện public và bạn fix nó từ fork của bạn trên Github, bạn cần phải cài đặt thư viện từ repository thay vì từ cái chính thức (cho đến khi bugfix được merge và phiên bản đã sửa lỗi được phát hành).

Điều này có thể được thực hiện dễ dàng bằng một [aliasing cùng dòng](https://getcomposer.org/doc/articles/aliases.md#require-inline-alias):

    
    
    {
        "repositories": [
            {
                "type": "vcs",
                "url": "https://github.com/you/monolog"
            }
        ],
        "require": {
            "symfony/monolog-bundle": "2.0",
            "monolog/monolog": "dev-bugfix as 1.0.x-dev"
        }
    }
    

Bạn có thể kiểm tra bugfix trên local trước khi push nó bằng cách [sử dụng `path` như là một kiểu repositoty](https://getcomposer.org/doc/05-repositories.md#path).

## Cập nhật 2018-01-08:

Sau khi công bố bài viết, tôi đã nhận được đề xuất về một số lời khuyên khác. Vì vậy, chúng đây:

## Lời khuyên #18: Cài đặt prestissimo để tăng tốc độ cài đặt packages

Có một plugin Composer [hirak/prestissimo](https://github.com/hirak/prestissimo) giúp tăng tốc độ cài đặt phụ thuộc bằng cách tải chúng song song.

Và điều tốt nhất là gì? Bạn chỉ cần cài đặt nó một lần, global và nó sẽ tự hoạt động trên toàn bộ project:

    
    
    composer global require hirak/prestissimo
    

## Lời khuyên #19: Kiểm tra ràng buộc phiên bản của bạn nếu bạn cảm thấy không chắc chắn.

Việc viết các ràng buộc phiên bản chính xác đôi khi có thể gây khó khăn ngay cả khi đọc [tài liệu](https://getcomposer.org/doc/articles/versions.md#writing-version-constraints).

May mắn thay, có một [Packagist Semver Checker](https://semver.mwl.be/) để bạn có thể kiểm tra phiên bản nào phù hợp với ràng buộc được chỉ định. Thay vì chỉ phân tích ràng buộc phiên bản, nó tải xuống dữ liệu từ Packagist để hiển thị cho các phiên bản được phát hành thực tế.

Xem [kết quả cho `symfony/symfony:^3.1`](https://semver.mwl.be/#?package=symfony%2Fsymfony&version=%5E3.1&minimum-stability=stable).

## Lời khuyên #20: Sử dụng authoritative class map trong production

Bạn nên [tạo authoritative class map](https://getcomposer.org/doc/articles/autoloader-optimization.md#optimization-level-2-a-authoritative-class-maps) trong production. Nó sẽ làm tăng tốc độ tải các class bằng cách include tất cả những thứ bên trong class-map và bỏ qua bất cứ kiểm tra filesystem nào.

Bạn có thể làm điều này bằng cách chạy nó như một phần của quá trình xây dựng production:

    
    
    composer dump-autoload --classmap-authoritative
    

## Lời khuyên #21: Cấu hình `autoload-dev` để tests

Bạn không muốn thêm các file test trong production class map (bởi vì kích thước file và bộ nhớ). Điều này có thể dễ dàng thực hiện bằng cách cấu hình `autoload-dev`
(tương tự như `autoload`):

    
    
    "autoload": {
        "psr-4": {
            "Acme\\": "src/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "Acme\\": "tests/"
        }
    },
    

## Lời khuyên #22: Thử sử dụng Composer scripts

Composer scripts là một công cụ nhẹ để tạo build scripts. Tôi đã viết [một bài viết riêng về vấn đề này](/have-you-tried-composer-scripts/).

